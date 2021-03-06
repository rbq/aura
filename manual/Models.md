title: Models
page_type: section
--
All models are Sequel models. Aura also uses the Sequel plugin system.

#### Creating a model
Subclass `Sequel::Model`.

    [app/models/movie.rb (ruby)]
    class Movie < Sequel::Model
      # ...
    end
  
#### Setting up migrations
Migrations are defined in `app/migrations/`. Use
[Sinatra-Sequel](http://github.com/rtomayko/sinatra-sequel)'s `migration`
method in your migrations files.

    [app/migrations/movie.rb (ruby)]
    class Main
      migration "foo v0.0.1 - create" do
        database.create_table do
          primary_key :id

          String :name
          String :description
          
          # ...
        end
      end
    end

#### Setting up plugins
Use Sequel's `plugin` class method.

    [app/models/movie.rb (ruby)]
    class Movie < Sequel::Model
      plugin :aura_editable
      plugin :aura_sluggable
      plugin :aura_hierarchy
    end

## Example

In your extension, create a model file like so.

    # extensions/myext/models/post.rb
    class Post < Sequel::Model

      # put guts here
      # for example:

      plugin :aura_editable
      plugin :aura_sluggable

      def shown_in_menu?() true; end
    end

