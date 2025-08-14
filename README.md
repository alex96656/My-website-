{
  "openapi": "3.1.0",
  "info": {
    "title": "Nekoweb API",
    "description": "The API allows you to interact with nekoweb server programmatically. You can use it to automate tasks like updating, creating and deleting files, and more.\n### Links\n- **Official docs:** [https://nekoweb.org/api](https://nekoweb.org/api)\n- **This website:** [https://github.com/mp-pinheiro/nekoweb-api-docs](https://github.com/mp-pinheiro/nekoweb-api-docs)\n- **Me:** [https://fairfruit.nekoweb.org](https://fairfruit.nekoweb.org)",
    "license": {
      "name": "Proprietary",
      "url": "https://web.archive.org/web/20240910041600/https://nekoweb.org"
    }
  },
  "servers": [
    {
      "url": "https://web.archive.org/web/20240910041600/https://nekoweb.org/api"
    }
  ],
  "tags": [
    {
      "name": "Site",
      "description": "Site related endpoints."
    },
    {
      "name": "Files",
      "description": "File related endpoints."
    },
    {
      "name": "Big Files",
      "description": "Big file related endpoints."
    }
  ],
  "components": {
    "securitySchemes": {
      "ApiKeyAuth": {
        "type": "apiKey",
        "in": "header",
        "name": "Authorization"
      }
    }
  },
  "security": [
    {
      "ApiKeyAuth": []
    }
  ],
  "paths": {
    "/site/info/{username}": {
      "get": {
        "tags": [
          "Site"
        ],
        "summary": "/site/info/:username",
        "description": "Get information about a user's site. Replace :username with the username of the user. This endpoint doesn't require auth if requested from Nekoweb site.\n\nReturns a JSON object with id, username, title, updates, followers, views, created_at and updated_at properties.\n\n**⚠ Note:** no need to provide an API key fro this request as the endpoint is public.",
        "parameters": [
          {
            "name": "username",
            "in": "path",
            "schema": {
              "type": "string"
            },
            "required": true,
            "example": "fairfruit"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "string",
                  "example": "application/json"
                }
              }
            },
            "content": {
              "application/json": {
                "schema": {
                  "type": "object"
                },
                "example": {
                  "id": 1855,
                  "username": "fairfruit",
                  "title": "Welcome to Fairfruit",
                  "updates": 5,
                  "followers": 0,
                  "views": 209,
                  "created_at": 1709235724576,
                  "updated_at": 1709597947291
                }
              }
            }
          }
        },
        "x-codeSamples": [
          {
            "lang": "Node",
            "source": "const fetch = require('node-fetch');\n\nlet url = 'https://web.archive.org/web/20240910041600/https://nekoweb.org/api/site/info/fairfruit';\n\nlet options = {\n  method: 'GET'\n};\n\nfetch(url, options)\n  .then(res => res)\n  .then(json => console.log(json))\n  .catch(err => console.error('error:' + err));"
          },
          {
            "lang": "Python",
            "source": "import requests\n\nurl = \"https://nekoweb.org/api/site/info/fairfruit\"\n\nresponse = requests.request(\"GET\", url)\n\nprint(response.text)"
          },
          {
            "lang": "Shell",
            "source": "curl --request GET \\\n  --url https://nekoweb.org/api/site/info/fairfruit"
          }
        ]
      }
    },
    "/files/create": {
      "post": {
        "tags": [
          "Files"
        ],
        "summary": "/files/create",
        "description": "Create a new file or folder.\n",
        "requestBody": {
          "content": {
            "application/x-www-form-urlencoded": {
              "schema": {
                "type": "object",
                "properties": {
                  "isFolder": {
                    "type": "boolean",
                    "example": "true"
                  },
                  "pathname": {
                    "type": "string",
                    "example": "test"
                  }
                }
              }
            }
          }
        },
        "parameters": [
          {
            "name": "Authorization",
            "in": "header",
            "schema": {
              "type": "string"
            },
            "example": "177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "string",
                  "example": "text/plain"
                }
              }
            },
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string"
                },
                "example": "Folder created"
              }
            }
          }
        },
        "x-codeSamples": [
          {
            "lang": "Node",
            "source": "const { URLSearchParams } = require('url');\nconst fetch = require('node-fetch');\nconst encodedParams = new URLSearchParams();\n\nencodedParams.set('isFolder', 'true');\nencodedParams.set('pathname', 'test');\n\nlet url = 'https://web.archive.org/web/20240910041600/https://nekoweb.org/api/files/create';\n\nlet options = {\n  method: 'POST',\n  headers: {\n    Authorization: '177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d',\n    'content-type': 'application/x-www-form-urlencoded'\n  },\n  body: encodedParams\n};\n\nfetch(url, options)\n  .then(res => res)\n  .then(json => console.log(json))\n  .catch(err => console.error('error:' + err));"
          },
          {
            "lang": "Python",
            "source": "import requests\n\nurl = \"https://nekoweb.org/api/files/create\"\n\npayload = \"isFolder=true&pathname=test\"\nheaders = {\n    \"Authorization\": \"177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d\",\n    \"content-type\": \"application/x-www-form-urlencoded\"\n}\n\nresponse = requests.request(\"POST\", url, data=payload, headers=headers)\n\nprint(response.text)"
          },
          {
            "lang": "Shell",
            "source": "curl --request POST \\\n  --url https://nekoweb.org/api/files/create \\\n  --header 'Authorization: 177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d' \\\n  --header 'content-type: application/x-www-form-urlencoded' \\\n  --data isFolder=true \\\n  --data pathname=test"
          }
        ]
      }
    },
    "/files/upload": {
      "post": {
        "tags": [
          "Files"
        ],
        "summary": "/files/upload",
        "description": "Upload a file or files. This will overwrite old files. Max 100MB.",
        "requestBody": {
          "content": {
            "multipart/form-data": {
              "schema": {
                "type": "object",
                "properties": {
                  "pathname": {
                    "type": "string",
                    "example": "/test"
                  },
                  "files": {
                    "type": "string",
                    "format": "binary",
                    "example": "@test.txt"
                  }
                }
              }
            }
          }
        },
        "parameters": [
          {
            "name": "Authorization",
            "in": "header",
            "schema": {
              "type": "string"
            },
            "example": "177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "string",
                  "example": "text/plain"
                }
              }
            },
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string"
                },
                "example": "Files uploaded"
              }
            }
          }
        },
        "x-codeSamples": [
          {
            "lang": "Node",
            "source": "const FormData = require('form-data');\nconst fetch = require('node-fetch');\nconst formData = new FormData();\n\nformData.append('pathname', '/test');\nformData.append('files', 'test.txt', { filepath: './test.txt' });\n\nlet url = 'https://web.archive.org/web/20240910041600/https://nekoweb.org/api/files/upload';\n\nlet options = {\n  method: 'POST',\n  headers: {\n    Authorization: '177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d'\n  }\n};\n\noptions.body = formData;\n\nfetch(url, options)\n  .then(res => res)\n  .then(json => console.log(json))\n  .catch(err => console.error('error:' + err));"
          },
          {
            "lang": "Python",
            "source": "import requests\n\nurl = \"https://nekoweb.org/api/files/upload\"\n\nfiles = {\"files\": \"test.txt\", open(\"path/to/test.txt\"), \"application/octet-stream\")} data = {\"pathname\": \"/test\"}\nheaders = {\n    \"Authorization\": \"177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d\"\n}\n\nresponse = requests.request(\"POST\", url, headers=headers, data=data, files=files)\n\nprint(response.text)"
          },
          {
            "lang": "Shell",
            "source": "curl --request POST \\\n  --url https://nekoweb.org/api/files/upload \\\n  --header 'Authorization: 177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d' \\\n  --form pathname=/test \\\n  --form files=@test.txt"
          }
        ]
      }
    },
    "/files/delete": {
      "post": {
        "tags": [
          "Files"
        ],
        "summary": "/files/delete",
        "description": "Delete a file or folder.",
        "requestBody": {
          "content": {
            "application/x-www-form-urlencoded": {
              "schema": {
                "type": "object",
                "properties": {
                  "pathname": {
                    "type": "string",
                    "example": "test"
                  }
                }
              }
            }
          }
        },
        "parameters": [
          {
            "name": "Authorization",
            "in": "header",
            "schema": {
              "type": "string"
            },
            "example": "177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "string",
                  "example": "text/plain"
                }
              }
            },
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string"
                },
                "example": "File/folder deleted"
              }
            }
          }
        },
        "x-codeSamples": [
          {
            "lang": "Node",
            "source": "const { URLSearchParams } = require('url');\nconst fetch = require('node-fetch');\nconst encodedParams = new URLSearchParams();\n\nencodedParams.set('pathname', 'test');\n\nlet url = 'https://web.archive.org/web/20240910041600/https://nekoweb.org/api/files/delete';\n\nlet options = {\n  method: 'POST',\n  headers: {\n    Authorization: '177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d',\n    'content-type': 'application/x-www-form-urlencoded'\n  },\n  body: encodedParams\n};\n\nfetch(url, options)\n  .then(res => res)\n  .then(json => console.log(json))\n  .catch(err => console.error('error:' + err));"
          },
          {
            "lang": "Python",
            "source": "import requests\n\nurl = \"https://nekoweb.org/api/files/delete\"\n\npayload = \"pathname=test\"\nheaders = {\n    \"Authorization\": \"177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d\",\n    \"content-type\": \"application/x-www-form-urlencoded\"\n}\n\nresponse = requests.request(\"POST\", url, data=payload, headers=headers)\n\nprint(response.text)"
          },
          {
            "lang": "Shell",
            "source": "curl --request POST \\\n  --url https://nekoweb.org/api/files/delete \\\n  --header 'Authorization: 177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d' \\\n  --header 'content-type: application/x-www-form-urlencoded' \\\n  --data pathname=test"
          }
        ]
      }
    },
    "/files/rename": {
      "post": {
        "tags": [
          "Files"
        ],
        "summary": "/files/rename",
        "description": "Rename/Move a file or folder.",
        "requestBody": {
          "content": {
            "application/x-www-form-urlencoded": {
              "schema": {
                "type": "object",
                "properties": {
                  "pathname": {
                    "type": "string",
                    "example": "test"
                  },
                  "newpathname": {
                    "type": "string",
                    "example": "test2"
                  }
                }
              }
            }
          }
        },
        "parameters": [
          {
            "name": "Authorization",
            "in": "header",
            "schema": {
              "type": "string"
            },
            "example": "177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "string",
                  "example": "text/plain"
                }
              }
            },
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string"
                },
                "example": "File/folder renamed"
              }
            }
          }
        },
        "x-codeSamples": [
          {
            "lang": "Node",
            "source": "const { URLSearchParams } = require('url');\nconst fetch = require('node-fetch');\nconst encodedParams = new URLSearchParams();\n\nencodedParams.set('pathname', 'test');\nencodedParams.set('newpathname', 'test2');\n\nlet url = 'https://web.archive.org/web/20240910041600/https://nekoweb.org/api/files/rename';\n\nlet options = {\n  method: 'POST',\n  headers: {\n    Authorization: '177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d',\n    'content-type': 'application/x-www-form-urlencoded'\n  },\n  body: encodedParams\n};\n\nfetch(url, options)\n  .then(res => res)\n  .then(json => console.log(json))\n  .catch(err => console.error('error:' + err));"
          },
          {
            "lang": "Python",
            "source": "import requests\n\nurl = \"https://nekoweb.org/api/files/rename\"\n\npayload = \"pathname=test&newpathname=test2\"\nheaders = {\n    \"Authorization\": \"177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d\",\n    \"content-type\": \"application/x-www-form-urlencoded\"\n}\n\nresponse = requests.request(\"POST\", url, data=payload, headers=headers)\n\nprint(response.text)"
          },
          {
            "lang": "Shell",
            "source": "curl --request POST \\\n  --url https://nekoweb.org/api/files/rename \\\n  --header 'Authorization: 177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d' \\\n  --header 'content-type: application/x-www-form-urlencoded' \\\n  --data pathname=test \\\n  --data newpathname=test2"
          }
        ]
      }
    },
    "/files/edit": {
      "post": {
        "tags": [
          "Files"
        ],
        "summary": "/files/edit",
        "description": "Edit a file.",
        "requestBody": {
          "content": {
            "multipart/form-data": {
              "schema": {
                "type": "object",
                "properties": {
                  "pathname": {
                    "type": "string",
                    "example": "test/test.txt"
                  },
                  "content": {
                    "type": "string",
                    "example": "Hello world"
                  }
                }
              }
            }
          }
        },
        "parameters": [
          {
            "name": "Authorization",
            "in": "header",
            "schema": {
              "type": "string"
            },
            "example": "177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "string",
                  "example": "text/plain"
                }
              }
            },
            "content": {
              "text/plain": {
                "schema": {
                  "type": "string"
                },
                "example": "File edited"
              }
            }
          }
        },
        "x-codeSamples": [
          {
            "lang": "Node",
            "source": "const FormData = require('form-data');\nconst fetch = require('node-fetch');\nconst formData = new FormData();\n\nformData.append('pathname', 'test/test.txt');\nformData.append('content', 'Hello world');\n\nlet url = 'https://web.archive.org/web/20240910041600/https://nekoweb.org/api/files/edit';\n\nlet options = {\n  method: 'POST',\n  headers: {\n    Authorization: '177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d'\n  }\n};\n\noptions.body = formData;\n\nfetch(url, options)\n  .then(res => res)\n  .then(json => console.log(json))\n  .catch(err => console.error('error:' + err));"
          },
          {
            "lang": "Python",
            "source": "import requests\n\nurl = \"https://nekoweb.org/api/files/edit\"\n\npayload = {'pathname': 'test/test.txt', 'content': 'Hello world'}\nheaders = {\n  'Authorization': 'bd77dda5279ddedde5615a90f6cdfeb51e7d49f107953ccc7ce30cdb8e54031b'\n}\n\nresponse = requests.request(\"POST\", url, headers=headers, data=payload)\n\nprint(response.text)"
          },
          {
            "lang": "Shell",
            "source": "curl --request POST \\\n  --url https://nekoweb.org/api/files/edit \\\n  --header 'Authorization: 177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d' \\\n  --form pathname=test/test.txt \\\n  --form 'content=Hello world'"
          }
        ]
      }
    },
    "/files/readfolder": {
      "get": {
        "tags": [
          "Files"
        ],
        "summary": "/files/readfolder",
        "description": "Read a folder.\n\nReturns a JSON array with objects like this: `{name: String, dir: Boolean}`",
        "parameters": [
          {
            "name": "Authorization",
            "in": "header",
            "schema": {
              "type": "string"
            },
            "example": "177e9b41e8b35b5e3cf90dd4a1ce90b9c8d1e6aa79863c0ebfd9c1e5dbb4d24d"
          },
          {
            "name": "pathname",
            "in": "query",
            "schema": {
              "type": "string"
            },
            "example": "test"
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "headers": {
              "Content-Type": {
                "schema": {
                  "type": "array"
                }
              }
            },
            "content": {
              "application/json": {
                "schema": {
                  "t