# How to use Rubocop configs
Reference the rubocop config that you want from another repo by inheriting from this file. When you are ready to upgrade rubocop to a different version, change the file you `inherit_from` in your repo's local `.rubocop.yml`.

Here is an example of what your repo's local `.rubocop.yml` will look like
```
inherit_from: https://raw.githubusercontent.com/q-centrix/style-guides/main/rubocop/.rubocop-0-77.yml
```

Note: Anything you add to your local yml file will overwrite what is in the inherited file. Read [the docs](https://docs.rubocop.org/rubocop/1.50/configuration.html#inheriting-from-another-configuration-file-in-the-project) for more information on precedence. This can be helpful if you want to add in something such as rubocop-rspec but want to disable/enable cops as you fix them over time.

### Other places you will need to check
#### Only the first time
1. `.codeclimate.yml`
    1. add a config file to the plugin so it will find the file in the correct place
        ```
        rubocop:
          enabled: true
          channel: rubocop-0-77
        ```
    2. Update the path that your fetched config will be saved to
        ```
          prepare:
            fetch:
              - url: "https://raw.githubusercontent.com/q-centrix/style-guides/main/rubocop/.rubocop-0-77.yml"
                path: ".rubocop-https---raw-githubusercontent-com-q-centrix-style-guides-main-rubocop--rubocop-0-77-yml"
          ```
2. `.gitgnore`
    1. remove `.rubocop.yml`
    2. add `.rubocop-https---raw-githubusercontent-com-q-centrix-style-guides-main-rubocop*`, this will ignore the file that gets created when you run rubocop

#### With every update
1. `.codeclimate.yml`
    1. Update the url fetched and the path, this should match the url you are inheriting from in your `rubocop.yml`
        ```
          prepare:
            fetch:
              - url: "https://raw.githubusercontent.com/q-centrix/style-guides/main/rubocop/.rubocop-0-77.yml"
                path: ".rubocop-https---raw-githubusercontent-com-q-centrix-style-guides-main-rubocop--rubocop-0-77-yml"
          ```
    2. The [rubocop channel](https://docs.codeclimate.com/docs/rubocop#using-rubocops-newer-versions) should specify the correct version. Available channels can be found [here](https://github.com/codeclimate/codeclimate-rubocop/branches/all?utf8=%E2%9C%93&query=channel%2Frubocop)
2. `.rubocop.yml`
    1. Update the url you are inheriting from. This should match the url in your `codeclimate.yml`
3. Make sure your `Gemfile` specifies the same version of rubocop as the config you are using.


# Contributing
Create a new directory for each type of style guide.
If the guides are version specific, like in rubocop, include the version number in the file name. Example: `.rubocop-1-23-0.yml`
