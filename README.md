# Rspec Api Blueprint

Autogeneration of API documentation using the Blueprint format from request specs.

You can find more about Blueprint at http://apiblueprint.org

## Installation

Add this line to your application's Gemfile:

    gem 'rspec_api_blueprint_2', require: false

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rspec_api_blueprint_2

## Usage

In your spec_helper.rb file add

    require 'rspec_api_blueprint_2'

Write tests using the following convention:

- Tests must be placed in `spec/requests` folder or they have to be tagged with `type: :request`
- Top level descriptions are named after the model (plural form) followed by the word “Requests”. For a example model called Arena it would be “Arenas Requests”.
- Second level descriptions are actions in the form of “VERB path”. For the show action of the Arenas controller it would be “GET /arenas/{id}”.

Example:

    describe 'Arenas Requests' do
      describe 'GET /v1/arenas/{id}' do
        it 'responds with the requested arena' do
          arena = create :arena, foursquare_id: '5104'
          get v1_arena_path(arena)

          expect(response).to have_http_status(:ok)
        end
      end
    end

The output:

    # GET /v1/arenas/{id}

    + Response 200 (application/json)

        {
          "arena": {
            "id": "4e9dbbc2-830b-41a9-b7db-9987735a0b2a",
            "name": "Clinton St. Baking Co. & Restaurant",
            "latitude": 40.721294,
            "longitude": -73.983994,
            "foursquare_id": "5104"
          }
        }

## Caveats

401, 403 and 301 statuses are ignored since rspec produces a undesired output.

TODO: Add option to choose ignored statuses.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
