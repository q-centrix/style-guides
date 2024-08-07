# How to use Rubocop configs
Reference the rubocop config that you want from another repo by inheriting from one of the `.rubocop-...` files.

Here is an example of what your repo's local `.rubocop.yml` will look like
```
inherit_from: https://raw.githubusercontent.com/q-centrix/style-guides/main/ruby/.rubocop-0-77.yml
```

Note: Anything you add to your local yml file will overwrite what is in the inherited file. Read [the docs](https://docs.rubocop.org/rubocop/1.50/configuration.html#inheriting-from-another-configuration-file-in-the-project) for more information on precedence. This can be helpful if you want to add in something such as rubocop-rspec but want to disable/enable cops as you fix them over time (see [auto gen configs](https://docs.rubocop.org/rubocop/configuration.html#automatically-generated-configuration)).

### Other places you will need to check
#### Only for the first implementation in a new project
1. `.codeclimate.yml`
    1. add a config file to the plugin so it will find the file in the correct place
        ```
        rubocop:
          enabled: true
          channel: rubocop-0-77
        ```
2. `.gitgnore`
    1. remove `.rubocop.yml`
    2. add `.rubocop-https*`, this will ignore the file that gets created when you run rubocop

#### With every update
When you are ready to upgrade rubocop to a different version, change the file you `inherit_from` in your repo's local `.rubocop.yml`.

1. `.rubocop.yml`
    1. Update the url you are inheriting from.
2. `.codeclimate.yml`
    1. Update the url fetched and the path, this should match the url you are inheriting from in your `rubocop.yml`
        ```
          prepare:
            fetch:
            - url: "https://raw.githubusercontent.com/q-centrix/style-guides/main/ruby/.rubocop-0-77.yml"
              path: ".rubocop-https---raw-githubusercontent-com-q-centrix-style-guides-main-ruby--rubocop-0-77-yml"
        ```
    2. The [rubocop channel](https://docs.codeclimate.com/docs/rubocop#using-rubocops-newer-versions) should specify the correct version. Available channels can be found [here](https://github.com/codeclimate/codeclimate-rubocop/branches/all?utf8=%E2%9C%93&query=channel%2Frubocop). **IMPORTANT NOTE: For version 1.60 you should use `beta` as the channel.**
        ```
          channel: rubocop-0-77
        ```
3. Make sure your `Gemfile` or `gemspec` specifies the same version of rubocop as the config you are using.
4. If you are going to use other rubocop gems (i.e. rubocop-rspec or rubocop-graphql) you need to add them to your gemfile. (These will also be listed under `require` at the top of the yml file)
    1. Starting with version 1.60 there is a comment at the bottom of the files stating which gems are needed.
    2. Remember to bundle update all of these additional gems.
