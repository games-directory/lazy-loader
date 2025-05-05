# LazyLoad

LazyLoad is being extracted from games.directory to provide you with a seamless, performant, lazy loader.

## Description

LazyLoad is a Ruby on Rails gem that enables effortless lazy loading of expensive operations in your Rails applications. It allows you to defer the execution of resource-intensive code until after the initial page load, significantly improving perceived performance.

Unlike other solutions that require custom routes and controllers, LazyLoad integrates directly with your existing controller actions and views, providing a clean, declarative syntax for defining and using lazy-loaded content.

## Key Features

- **Simple DSL**: Define lazy operations directly in your controller actions
- **Flexible View Helpers**: Multiple syntax options for lazy loading in your views
- **Auto-loading**: Content loads automatically when needed
- **Stimulus Integration**: Built with Stimulus for smooth JavaScript interactions
- **No Custom Routes**: Middleware handles all requests automatically
- **Preserves Context**: Lazy operations execute in the full controller context with access to all variables
- **Multiple Loading Strategies**: Support for different loading behaviors

## Usage Examples

### In Controllers

```ruby
class DashboardController < ApplicationController
  # Define a named data source
  lazy_data_source :activity_feed do
    ActivityService.for_user(current_user)
  end
  
  def index
    @users = User.all
    
    # Define a lazy operation within the action
    lazy do
      @expensive_chart = @users.some_expensive_operation
    end
  end
```

### In Views

```erb
<!-- Simple usage with a named data source -->
<%= lazy_load :activity_feed %>

<!-- With variables from a lazy operation in the controller -->
<%= lazy_load variables: [:expensive_chart] %>

<!-- With custom content -->
<%= lazy_load :activity_feed do %>
  <div class="feed">
    <% @activity_feed.each do |activity| %>
      <div class="activity-item"><%= activity.description %></div>
    <% end %>
  </div>
<% end %>
```

### Performance Benefits

- Faster Initial Page Load: Render critical content first
- Improved Perceived Performance: Page becomes interactive sooner
- Reduces Server Load: Expensive operations only run when needed
- Better User Experience: Content appears progressively

## Installation
