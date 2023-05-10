# How to use Rubocop configs
Reference the rubocop config that you want from another repo by inheriting from this file. When you are ready to upgrade rubocop to a different version, change the file you `inherit_from` in your repo's local `.rubocop.yml`.

Here is an example of what your repo's local `.rubocop.yml` will look like
```
inherit_from: https://raw.githubusercontent.com/q-centrix/style-guides/main/rubocop/.rubocop-0-77.yml
```

Note: Anything you add to your local yml file will overwrite what is in the inherited file. Read [the docs](https://docs.rubocop.org/rubocop/1.50/configuration.html#inheriting-from-another-configuration-file-in-the-project) for more information on precedence. This can be helpful if you want to add in something such as rubocop-rspec but want to disable/enable cops as you fix them over time.

### Other places you will need to check
#### Only the first time
- Add the following to your `.gitgnore` `.rubocop-https---raw-githubusercontent-com-q-centrix-style-guides-main-rubocop*`, this will ignore the file that gets created when you run rubocop locally
- Do not gitignore your `.rubocop.yml`
- In your `.codeclimate.yml`, make sure you are NOT referencing this file. It will use your local `.rubocop.yml` by default, and that will reference this file.

#### With every update
- Make sure your `Gemfile` specifies the same version of rubocop as the config you are using.
- In `.codeclimate.yml` the [rubocop channel](https://docs.codeclimate.com/docs/rubocop#using-rubocops-newer-versions) should specify the correct version. Available channels can be found [here](https://github.com/codeclimate/codeclimate-rubocop/branches/all?utf8=%E2%9C%93&query=channel%2Frubocop)
  ```
    rubocop:
      enabled: true
      channel: rubocop-0-77
  ```



# Contributing
Create a new directory for each type of style guide.
If the guides are version specific, like in rubocop, include the version number in the file name. Example: `.rubocop-1-23-0.yml`
