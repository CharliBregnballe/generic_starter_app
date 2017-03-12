# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...



Example of Faker and FactoryGirl:

```ruby

***spec/factories/contacts.rb***

FactoryGirl.define do
  factory :contact do
    full_name     { Faker::Name.name }
    email         { Faker::Internet.email }
    phone_number  { Faker::PhoneNumber.phone_number }
    address       { Faker::Address.street_address }
  end
end

```

Example of model test

```ruby

***spec/models/contact_spec.rb***

require 'rails_helper'

RSpec.describe Contact, type: :model do
  it "has a valid factory" do
    expect(contact).to be_valid
  end
end

```

Example of controller test

```ruby

***spec/controllers/contacts_controller_spec.rb***

require 'rails_helper'

RSpec.describe ContactsController, type: :controller do

  describe "POST #create" do
    context "with valid attributes" do
      it "create new contact" do
        post :create, contact: attributes_for(:contact)
        expect(Contact.count).to eq(1)
      end
    end
  end
end

```

Feature spec (Create)

```ruby

***spec/features/contacts/create_spec.rb***
require 'rails_helper'

RSpec.feature "Contact", :type => :feature do
  scenario "Create a new contact" do
    visit "/contacts/new"

    fill_in "Full name", :with => "My Name"
    fill_in "Email", :with => "my@email.com"
    fill_in "Phone number", :with => "123456789"
    fill_in "Address", :with => "34, Allen Way, OA"

    click_button "Create Contact"

    expect(page).to have_text("My Name")
  end
end

```

Consider using simplecov to check how much of the app is covered by tests:

gem 'simplecov', :require => false

Run bundle install.

Next open your spec helper are require simplecov

require 'simplecov'
SimpleCov.start
