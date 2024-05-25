# Chung Kevin Modification 

There is a unit test error in the server section. That part is commented out.
I have raised the issue in the original repo, waiting for response.

# Steps
1. Git clone the project.
2. cd to zally server folder
3. run project
4. prepare the open-api definition string (convert to string). Key is "api_definition_string", value is the converted value.
   ```
   {
    "api_definition_string": "{\"openapi\":\"3.0.1\",\"info\":{\"title\":\"My Spring 3 OPENAPI DEMO APP\",\"description\":\"This is a demo app for using swagger 3 openapi\",\"version\":\"1.0.0\",\"x-audience\":\"component-internal\",\"x-api-id\":\"23131312312\"},\"servers\":[{\"url\":\"http://localhost:8083\",\"description\":\"Generated server url\"}],\"security\":[{\"globalHeader\":[]},{\"globalBearer\":[]}],\"paths\":{\"/users/{id}\":{\"get\":{\"tags\":[\"user-controller\"],\"operationId\":\"getUserById\",\"parameters\":[{\"name\":\"id\",\"in\":\"path\",\"required\":true,\"schema\":{\"minimum\":1,\"type\":\"integer\",\"format\":\"int64\"}}],\"responses\":{\"200\":{\"description\":\"OK\",\"content\":{\"*/*\":{\"schema\":{\"$ref\":\"#/components/schemas/User\"}}}}}},\"put\":{\"tags\":[\"user-controller\"],\"operationId\":\"updateUserById\",\"parameters\":[{\"name\":\"id\",\"in\":\"path\",\"required\":true,\"schema\":{\"minimum\":1,\"type\":\"integer\",\"format\":\"int64\"}}],\"requestBody\":{\"content\":{\"application/json\":{\"schema\":{\"$ref\":\"#/components/schemas/User\"}}},\"required\":true},\"responses\":{\"200\":{\"description\":\"OK\",\"content\":{\"*/*\":{\"schema\":{\"$ref\":\"#/components/schemas/User\"}}}}}},\"delete\":{\"tags\":[\"user-controller\"],\"operationId\":\"deleteUserById\",\"parameters\":[{\"name\":\"id\",\"in\":\"path\",\"required\":true,\"schema\":{\"type\":\"integer\",\"format\":\"int64\"}}],\"responses\":{\"200\":{\"description\":\"OK\",\"content\":{\"*/*\":{\"schema\":{\"type\":\"boolean\"}}}}}}},\"/users\":{\"get\":{\"tags\":[\"user-controller\"],\"operationId\":\"getUsers\",\"responses\":{\"200\":{\"description\":\"OK\",\"content\":{\"*/*\":{\"schema\":{\"type\":\"array\",\"items\":{\"$ref\":\"#/components/schemas/User\"}}}}}}},\"post\":{\"tags\":[\"user-controller\"],\"operationId\":\"createNewUser\",\"requestBody\":{\"content\":{\"application/json\":{\"schema\":{\"$ref\":\"#/components/schemas/User\"}}},\"required\":true},\"responses\":{\"200\":{\"description\":\"OK\",\"content\":{\"*/*\":{\"schema\":{\"$ref\":\"#/components/schemas/User\"}}}}}}}},\"components\":{\"schemas\":{\"Address\":{\"type\":\"object\",\"properties\":{\"street\":{\"type\":\"string\"},\"suite\":{\"type\":\"string\"},\"city\":{\"type\":\"string\"},\"zipcode\":{\"type\":\"string\"},\"geo\":{\"$ref\":\"#/components/schemas/Geo\"}}},\"Company\":{\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\"},\"catchPhrase\":{\"type\":\"string\"},\"bs\":{\"type\":\"string\"}}},\"Geo\":{\"type\":\"object\",\"properties\":{\"lat\":{\"type\":\"string\"},\"lng\":{\"type\":\"string\"}}},\"User\":{\"required\":[\"address\",\"name\",\"username\"],\"type\":\"object\",\"properties\":{\"id\":{\"type\":\"integer\",\"format\":\"int64\"},\"name\":{\"type\":\"string\"},\"username\":{\"maxLength\":200,\"minLength\":8,\"type\":\"string\"},\"email\":{\"type\":\"string\"},\"address\":{\"$ref\":\"#/components/schemas/Address\"},\"phone\":{\"type\":\"string\"},\"website\":{\"type\":\"string\"},\"company\":{\"$ref\":\"#/components/schemas/Company\"}}}},\"securitySchemes\":{\"globalHeader\":{\"type\":\"apiKey\",\"name\":\"global-header-name\",\"in\":\"header\"},\"globalBearer\":{\"type\":\"http\",\"scheme\":\"bearer\"}}}}"
}
   ```



# Steps Here (Obselete)
Run following command.
```bash
docker compose up -d
```

Then check the docker process, make sure zally server is running. For UI, we can ignore since it is not working.

After that, we can start sent post request to use api linting. **Change the data section to your swagger json fil**e.


```cURL
curl --location 'localhost:8000/api-violations' \
--header 'Content-Type: application/json' \
--data '{
  "openapi": "3.0.1",
  "api_definition_string": "openapi: 3.0.2",
  "info": {
    "title": "My Spring 3 OPENAPI DEMO APP",
    "description": "This is a demo app for using swagger 3 openapi",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "http://localhost:8083",
      "description": "Generated server url"
    }
  ],
  "security": [
    {
      "globalHeader": []
    },
    {
      "globalBearer": []
    }
  ],
  "paths": {
    "/users/{id}": {
      "put": {
        "tags": [
          "user-controller"
        ],
        "operationId": "updateUserById",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/User"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "*/*": {
                "schema": {
                  "$ref": "#/components/schemas/User"
                }
              }
            }
          }
        }
      },
      "delete": {
        "tags": [
          "user-controller"
        ],
        "operationId": "deleteUserById",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "*/*": {
                "schema": {
                  "type": "boolean"
                }
              }
            }
          }
        }
      }
    },
    "/users": {
      "get": {
        "tags": [
          "user-controller"
        ],
        "operationId": "getUsers",
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "*/*": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/User"
                  }
                }
              }
            }
          }
        }
      },
      "post": {
        "tags": [
          "user-controller"
        ],
        "operationId": "createNewUser",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/User"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "*/*": {
                "schema": {
                  "$ref": "#/components/schemas/User"
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "Address": {
        "type": "object",
        "properties": {
          "street": {
            "type": "string"
          },
          "suite": {
            "type": "string"
          },
          "city": {
            "type": "string"
          },
          "zipcode": {
            "type": "string"
          },
          "geo": {
            "$ref": "#/components/schemas/Geo"
          }
        }
      },
      "Company": {
        "type": "object",
        "properties": {
          "name": {
            "type": "string"
          },
          "catchPhrase": {
            "type": "string"
          },
          "bs": {
            "type": "string"
          }
        }
      },
      "Geo": {
        "type": "object",
        "properties": {
          "lat": {
            "type": "string"
          },
          "lng": {
            "type": "string"
          }
        }
      },
      "User": {
        "required": [
          "address",
          "name",
          "username"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          },
          "username": {
            "maxLength": 200,
            "minLength": 8,
            "type": "string"
          },
          "email": {
            "type": "string"
          },
          "address": {
            "$ref": "#/components/schemas/Address"
          },
          "phone": {
            "type": "string"
          },
          "website": {
            "type": "string"
          },
          "company": {
            "$ref": "#/components/schemas/Company"
          }
        }
      }
    },
    "securitySchemes": {
      "globalHeader": {
        "type": "apiKey",
        "name": "global-header-name",
        "in": "header"
      },
      "globalBearer": {
        "type": "http",
        "scheme": "bearer"
      }
    }
  }
}'
```

How to get your project swagger json file?

After spinning up your application, visit http://localhost:8080/swagger-ui/index.html#/

Click the docs link, then you will get the swagger json file.

> Note: Zally requires `"api_definition_string": "openapi: 3.0.2",` in payload. Please add this into your swagger json.


# Zally: A minimalistic, simple-to-use OpenAPI 2 and 3 linter

[![Build Status](https://travis-ci.org/zalando/zally.svg?branch=master)](https://travis-ci.org/zalando/zally)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/05a7515011504c06b1cb35ede27ac7d4)](https://www.codacy.com/app/zally/zally?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=zalando/zally&amp;utm_campaign=Badge_Grade)
[![Join the chat at https://gitter.im/zalando/zally](https://badges.gitter.im/zalando/zally.svg)](https://gitter.im/zalando/zally?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

<img src="logo.png" width="200" height="200" />

Zally is a quality assurance tool. It's a linter for OpenAPI specifications,
it performs the following tasks : 

- Increases the quality of APIs
- Checks compliance
- Delivers early feedback for API designers
- Ensures the same look-and-feel of APIs
- Supports [API-First approach](https://opensource.zalando.com/restful-api-guidelines/#100)
- Provides best practices and advices

Its standard configuration will check your APIs against the rules defined in
[Zalando's RESTful Guidelines](http://zalando.github.io/restful-api-guidelines/),
but anyone can use it **out-of-the-box**.

Zally has an easy-to-use [CLI](cli/README.md) which uses the server in the background so that
you can check your API *on the spot*. It also features an intuitive
[Web UI](web-ui/README.md) that shows implemented rules and lints external files
and (with its online editor) API definitions.

## Features

- Support for OpenAPI 3 and (Swagger) OpenAPI 2 specifications
- RESTful API, CLI and Web interface
- Rich Check configuration
- Ignore functionality (`x-zally-ignore` extension)
- Java/Kotlin API for new Checks + helper functions

## Quick start guide

Trying out Zally is easy. You can build and run the whole Zally stack (web-ui, server
and database) by executing:

```bash
docker compose up -d
```

Web UI is accessible on `http://localhost:8080`; Zally server on `http://localhost:8000`

## Documentation and Manuals

Please consult the following documents for further information:

- [Zally Concepts](documentation/concepts.md)
- [How to operate](documentation/operation.md) Zally tools
- [How to use Zally](documentation/usage.md)
- [How to develop new Rules](documentation/rule-development.md)
- [Building Under Windows Subsystem for Linux](documentation/build-under-wsl.md)

## Integrations

- [Zally Maven Plugin](https://github.com/ethlo/zally-maven-plugin) (unofficial)

## Contributing to Zally

Zally welcomes contributions from the open source community. To get started, take a
look at our [contributing guidelines](CONTRIBUTING). Then check our
[Project Board](https://github.com/zalando/zally/projects/1) and
[Issues Tracker](https://github.com/zalando/zally/issues) for ideas.

## Contact

Feel free to join our [Gitter room](https://gitter.im/zalando/zally) or contact one
of the [maintainers](MAINTAINERS) directly.

## Alternatives 

Zally is not the only linter for OpenAPI v2 and v3. There is [an article](https://nordicapis.com/8-openapi-linters/) comparing different OpenAPI linters.

So why should you choose Zally?
- It supports [Zalando's RESTful Guidelines](http://zalando.github.io/restful-api-guidelines/)
- It can be used in multiple ways: RESTful API, CLI and Web interface
- Highly customizable (with Kotlin)  

## License

MIT license with an exception. See [license file](LICENSE).

## Publish

### Prerequisites

* [Signing plugin](https://docs.gradle.org/current/userguide/signing_plugin.htm) configured
* `OSSRH_JIRA_USERNAME` and `OSSRH_JIRA_PASSWORD` environment variables to access [Maven Central Repo](https://oss.sonatype.org/) are 
configured

### Steps

1. Create a separate branch with a name `release-<release-version>`.
2. Update current version in `server/gradle.properties` from `-SNAPSHOT` to a final version.
3. Update mime types configuration:
   ```shell
      ./gradlew -q generate-media-types-config --info
   ```
4. Commit the updated file to the repository.
5. Release Zally server and API using the command
   ```
   cd server
   ./gradlew clean build publishAllPublicationsToMavenRepository
   ```
6. Commit `server/gradle.properties` with the release version
7. Create a tag
    ```shell script
    git tag v<release-version> -m "Version <release-version>"
    ```
8. Bump version in `server/gradle.properties` to the next `-SNAPSHOT`

9. Push `release` branch and tag
   ```shell script
    git push origin
    git push origin <tag-name>
   ```
10. Create a Pull Request with the version update
11. Create and publish a release with a new version in GitHub
