# {{cookiecutter.app_name}}

{{cookiecutter.project_short_description}}



## Env Variables KEYS and DESCRIPTION

| Name           | Description                                     | Required | Default |
| -------------- | ----------------------------------------------- | -------- | ------- |
| **PROJECT_ID** | Google Cloud Project ID.                        | Y        | -       |
| **ENV**        | Env (dev, test, pro) for logging configuration. | Y        | -       |
| **LOG_LEVEL**  | Logging level (info, debug).                    | N        | info    |
| **HTTP_PORT**  | Http port service listens to.                   | N        | 8080    |


### GCP Permissions
The Service Account must have the following roles:
- 
- 


## Authors


| Name                          | Role              | Slack                                               | Email                                                                   |
| ----------------------------- | ----------------- | --------------------------------------------------- | ----------------------------------------------------------------------- |
| **{{cookiecutter.app_name}}** | Software Engineer | [Slack](https://novafutur.slack.com/team/UJELJSFNY) | [{{cookiecutter.email_address}}](mailto:{{cookiecutter.email_address}}) |
