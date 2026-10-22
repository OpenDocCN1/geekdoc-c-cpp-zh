

```ruby
def self.authenticate(name, password)
  user = self.find_by_name(name)
  if user
    expected_password = encrypted_password(password, user.salt)
    if user.hashed_password != expected_password
      user = nil
    end
  end
  user
end

# 'password' is a virtual attribute
def password
  @password
end

def password=(pwd)
  @password = pwd
  return if pwd.blank?
  create_new_salt
  self.hashed_password = User.encrypted_password(self.password, self.salt)
end

def after_destroy
  if User.count.zero?
    raise "Can't delete last user"
  end
end

private

def password_non_blank
  errors.add(:password, "Missing password") if hashed_password.blank?
end

def create_new_salt
  self.salt = self.object_id.to_s + rand.to_s
end

def self.encrypted_password(password, salt)
  string_to_hash = password + "wibble" + salt
  Digest::SHA1.hexdigest(string_to_hash)
end
```

## 布局和视图

`Download depot_f/app/views/layouts/store.html.erb`

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
                      "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html>
<head>
  <title>Pragprog Books Online Store</title>
  <%= stylesheet_link_tag "depot", :media => "all" %>
```

```
<%= javascript_include_tag :defaults %>
</head>
<body id="store">
<div id="banner">
  <%= form_tag '', :method => 'GET', :class => 'locale' do %>
    <%= select_tag 'locale', options_for_select(LANGUAGES, I18n.locale),
      :onchange => 'this.form.submit()' %>
    <%= submit_tag 'submit' %>
    <%= javascript_tag "$('.locale input').each(Element.hide)" %>
  <% end %>
  <%= image_tag("logo.png") %>
  <%= @page_title || I18n.t('layout.title') %>
</div>
<div id="columns">
  <div id="side">
    <% if @cart %>
      <% hidden_div_if(@cart.items.empty?, :id => "cart") do %>
        <%= render(:partial => "cart", :object => @cart) %>
      <% end %>
    <% end %>

    <a href="http://www...."> <%= I18n.t 'layout.side.home' %> </a><br />
    <a href="http://www..../faq"> <%= I18n.t 'layout.side.questions' %> </a><br />
    <a href="http://www..../news"> <%= I18n.t 'layout.side.news' %> </a><br />
    <a href="http://www..../contact"> <%= I18n.t 'layout.side.contact' %> </a><br />
    <% if session[:user_id] %>
      <br />
      <%= link_to 'Orders', :controller => 'orders' %><br />
      <%= link_to 'Products', :controller => 'products' %><br />
      <%= link_to 'Users', :controller => 'users' %><br />
      <br />
      <%= link_to 'Logout', :controller => 'admin', :action => 'logout' %>
    <% end %>
  </div>
  <div id="main">
    <% if flash[:notice] -%>
      <div id="notice"><%= flash[:notice] %></div>
    <% end -%>

    <%= yield :layout %>
  </div>
</div>
</body>
</html>
```

## 管理员视图

Download depot_t/app/views/admin/index.html.erb

```
<h1>Welcome</h1>

It's <%= Time.now %>
We have <%= pluralize(@total_orders, "order") %>.

```

```
Download depot_f/app/views/admin/login.html.erb
<div class="depot-form">
  <% form_tag do %>
    <fieldset>
      <legend>Please Log In</legend>

      <div>
        <label for="name">Name:</label>
        <%= text_field_tag :name, params[:name] %>
      </div>

      <div>
        <label for="password">Password:</label>
        <%= password_field_tag :password, params[:password] %>
      </div>

      <div>
        <%= submit_tag "Login" %>
      </div>
    </fieldset>
  <% end %>
</div>
```

```
Download depot_f/app/views/admin/login.html.erb
<div class="depot-form">
  <% form_tag do %>
    <fieldset>
      <legend>Please Log In</legend>

      <div>
        <label for="name">Name:</label>
        <%= text_field_tag :name, params[:name] %>
      </div>

      <div>
        <label for="password">Password:</label>
        <%= password_field_tag :password, params[:password] %>
      </div>

      <div>
        <%= submit_tag "Login" %>
      </div>
    </fieldset>
  <% end %>
</div>
```

## 产品视图

```
Download depot_f/app/views/products/edit.html.erb
<h1>Editing product</h1>

<% form_for(@product) do |f| %>
  <%= f.error_messages %>
```

```
<p>
  <%= f.label :title %><br />
  <%= f.text_field :title %>
</p>
<p>
  <%= f.label :description %><br />
  <%= f.text_area :description %>
</p>
<p>
  <%= f.label :image_url %><br />
  <%= f.text_field :image_url %>
</p>
<p>
  <%= f.label :price %><br />
  <%= f.text_field :price %>
</p>
<p>
  <%= f.submit "Update" %>
</p>
<% end %>

<%= link_to 'Show', @product %> |
<%= link_to 'Back', products_path %>

Download depot_t/app/views/products/index.html.erb

<div id="product-list">
  <h1>Listing products</h1>

  <table>
  <% for product in @products %>
    <tr class="<%= cycle('list-line-odd', 'list-line-even') %>">

      <td>
        <%= image_tag product.image_url, :class => 'list-image' %>
      </td>

      <td class="list-description">
        <dl>
          <dt><%=h product.title %></dt>
          <dd><%=h truncate(product.description.gsub(/<.*?>/,''),
            :length => 80) %></dd>
        </dl>
      </td>

      <td class="list-actions">
        <%= link_to 'Show', product %><br />
        <%= link_to 'Edit', edit_product_path(product) %><br />
        <%= link_to 'Destroy', product,
          :confirm => 'Are you sure?',
          :method => :delete %>
      </td>
    </tr>
  <% end %>

```

```
</table>
</div>

<br />

<%= link_to 'New product', new_product_path %>
Download depot_t/app/views/products/new.html.erb
<h1>New product</h1>

<%= form_for(@product) do |f| %>
  <%= f.error_messages %>

  <p>
    <%= f.label :title %><br />
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :description %><br />
    <%= f.text_area :description, :rows => 6 %>
  </p>
  <p>
    <%= f.label :image_url %><br />
    <%= f.text_field :image_url %>
  </p>
  <p>
    <%= f.label :price %><br />
    <%= f.text_field :price %>
  </p>

  <p>
    <%= f.submit "Create" %>
  </p>
<% end %>

<%= link_to 'Back', products_path %>
Download depot_t/app/views/products/show.html.erb
<p>
  <b>Title:</b>
  <%=h @product.title %>
</p>

<p>
  <b>Description:</b>
  <%= @product.description %>
</p>

<p>
  <b>Image url:</b>
  <%=h @product.image_url %>
</p>
```

```
<p>
  <b>Price:</b>
  <%=h @product.price %>
</p>

<%= link_to 'Edit', edit_product_path(@product) %> |
<%= link_to 'Back', products_path %>
```

## 商店视图

```
Download depot1/app/views/store/_cart.html.erb
```

```
<div class="cart-title"><%= I18n.t 'layout.cart.title' %></div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
  </tr>
</table>

<%= button_to I18n.t('layout.cart.button.checkout'), :action => 'checkout' %>
<%= button_to I18n.t('layout.cart.button.empty'), :action => :empty_cart %>
```

```
Download depot1/app/views/store/_cart_item.html.erb
```

```
<% if cart_item == @current_item %>
<tr id="current_item">
<% else %>
<tr>
<% end %>
<td><%= cart_item.quantity %>&times;</td>
<td><%=h cart_item.title %></td>
<td class="item-price"><%= number_to_currency(cart_item.price) %></td>
</tr>
```

```
Download depot1/app/views/store/add_to_cart.js.rjs
```

```
page.select("div#notice").each { |div| div.hide }

page.replace_html("cart", :partial => "cart", :object => @cart)

page[:cart].visual_effect :blind_down if @cart.total_items == 1

page[:current_item].visual_effect :highlight,
  :startcolor => "#88ff88",
  :endcolor => "#114411"
```

```
Download depot1/app/views/store/checkout.html.erb
```

```
<div class="depot-form">

  <%= error_messages_for 'order' %>
```

```
<% form_for :order, :url => { :action => :save_order } do |form| %>
  <fieldset>
    <legend><%= I18n.t 'checkout.legend' %></legend>

    <div>
      <%= form.label :name, I18n.t('checkout.name') + ":" %>
      <%= form.text_field :name, :size => 40 %>
    </div>

    <div>
      <%= form.label :address, I18n.t('checkout.address') + ":" %>
      <%= form.text_area :address, :rows => 3, :cols => 40 %>
    </div>

    <div>
      <%= form.label :email, I18n.t('checkout.email') + ":" %>
      <%= form.text_field :email, :size => 40 %>
    </div>

    <div>
      <%= form.label :pay_type, I18n.t('checkout.pay_type') + ":" %>
      <%= form.select :pay_type,
                      Order::PAYMENT_TYPES,
                      :prompt => I18n.t('checkout.pay_prompt') %>
    </div>

    <%= submit_tag I18n.t('checkout.submit'), :class => "submit" %>
  </fieldset>
<% end %>
</div>
Download depot_t/app/views/store/index.html.erb
<h1><%= I18n.t 'main.title' %></h1>

<% for product in @products %>
  <div class="entry">
    <%= image_tag(product.image_url) %>
    <h3><%=h product.title %></h3>
    <%= product.description %>
    <div class="price-line">
      <span class="price"><%= number_to_currency(product.price) %></span>
      <% form_remote_tag :url => {:action => 'add_to_cart', :id => product} do %>
        <%= submit_tag I18n.t('main.button.add') %>
      <% end %>
    </div>
  </div>
<% end %>
```
