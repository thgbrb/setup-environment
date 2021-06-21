## Load env files and load values to environment variable
Sometimes a monorepo can be challenging, like handle config files or group configs.
The proposal of this action is read an env file and load values to environment variables.

### Sections
Sections groups variables. It means an env files can handle keys for more than one application, even it cotains key with same name.


### Create env files
An env files is a file in a format of key=value. The action reads this file and load key=values to environment variables.

```dotenv 
KEY_NAME=value

[SECTION]
Key.structured:name=value_of_key
VALUE_WITH_SPACES=Dev Lorem Ipsum
```

> **Important**
>
> Env files must reside in git root folders!

### Add setup-environment action to workflow
Once an env file is created, action are ready to use it.

```yaml
- name: Load release-candidate vars
  id: set_env_release-candidate
  if: github.ref == 'refs/heads/release-candidate'
  uses: ./.github/actions/setup-environment
    with:
      environment-config-file: "setup_qa.env"
      section-name: "API_LOREM_IPSUM"
# In this example, all key from default section and
# grouped into section named API_LOREM_IPSUM will be loaded to environment variables.
```
For more informations how to use [have a look in this repo workflow](.github/workflows/main.yml)
