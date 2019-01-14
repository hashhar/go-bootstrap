# All possible ways to install software

## Official repositories

Should be installable with just `$PKG_MGR pkgname`. eg. **apt**, **brew**

Both **apt** and **brew** have the same interface.

### Inputs

- **Ubuntu**
  - Array of packages
- **MacOS**
  - Array of packages

## Third party repositories

Should be installable with just `$PKG_MGR pkgname` after the third party
repositories have been added. eg. **brew tap**, **apt-add-repository**,
**apt-key**

Both **apt** and **brew** have the same interface.

### Inputs

- **Ubuntu**
  - **apt-add-repository**
    - `ppa:user/repo`
    - `deb url ${LINUX_RELEASE} section`
  - **apt-key**
    - URL of key
    - Key fingerprint
  - **apt install ./deb**
    - URL of deb file
- **MacOS**
  - `user/repo` to tap
  - `cask::pkgname`

## Pre-built packages

### Packages installable using some other package manager

**gem install**, **pip install**, **npm install**, **go get**

All the above have the same interface (they all accept a package specification
as the argument).

#### Inputs

- Array of packages with protocol identifier

## Pre-built archive

Should be installed with just expanding the archive to a location. eg. **dmg**,
**prebuilt.tar.gz**.

Have the same interface irrespective of the OS.

### Inputs

- URL to download a archive.
- Array of shell commands to execute / Shell script in a multiline string to
  execute

## Compile from source

### Source in archive

Should be installed by expanding the archive and executing a given shell script.

- URL to download archive
- Array of shell commands to execute / Shell script in a multiline string to
  execute

### Source in git

Should be installed by cloning the code and executing a given shell script.

- Clone URL
- Array of shell commands to execute / Shell script in a multiline string to
  execute

# Sample JSON

```json
{
    "name": "dummy",
    "ubuntu": {
        "packaged": {
            "packages": [
                "official_repo",
                "ppa_pkg",
                "apt_repo",
                "https://example.org/deb_file.deb"
            ],
            "repositories": [
                "ppa:ppa_user/ppa_pkg",
                "deb https://example.org/debian ${LINUX_RELEASE} main"
            ],
            "keys": [
                "https://example.org/key.asc",
                "0C49F3730359A14518585931BC711F9BA15703C6"
            ]
        },
        "prebuilt": {
            "sources": [
                "https://example.org/pkg.tar.gz"
            ],
            "install": [
                "sudo tar -xvf pkg.tar.gz -C /opt",
                "sudo chown -R $USER:$USER /opt/pkg"
            ]
        },
        "source": {
            "sources": [
                "https://example.org/pkg.source.tar.gz",
                "https://github.com/example/pkg.git"
            ],
            "install": [
                "sudo tar -xvf pkg.source.tar.gz -c /tmp",
                "cd /tmp/pkg.source",
                "sudo make install",
                "cd pkg",
                "./configure",
                "sudo make install"
            ]
        },
        "post_install": "Please read release notes at https://example.org"
    },
    "macos": {
        "packaged": {
            "packages": [
                "official_repo",
                "cask::cask_software",
                "user_repo_software"
            ],
            "repositories": [
                "user/repo"
            ]
        },
        "prebuilt": {
            "sources": [
                "https://example.org/pkg.tar.gz"
            ],
            "install": [
                "sudo tar -xvf pkg.tar.gz -C /opt",
                "sudo chown -R $USER:$USER /opt/pkg"
            ]
        },
        "source": {
            "sources": [
                "https://example.org/pkg.source.tar.gz",
                "https://github.com/example/pkg.git"
            ],
            "install": [
                "sudo tar -xvf pkg.source.tar.gz -c /tmp",
                "cd /tmp/pkg.source",
                "sudo make install",
                "cd pkg",
                "./configure",
                "sudo make install"
            ]
        },
        "post_install": "Please read release notes at https://example.org"
    }
}
```

And the corresponding JSON schema generated using https://www.liquid-technologies.com/online-json-to-schema-converter

```json
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "name": {
            "type": "string"
        },
        "ubuntu": {
            "type": "object",
            "properties": {
                "packaged": {
                    "type": "object",
                    "properties": {
                        "packages": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "repositories": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "keys": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        }
                    },
                    "required": [
                        "packages"
                    ]
                },
                "prebuilt": {
                    "type": "object",
                    "properties": {
                        "sources": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "install": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        }
                    },
                    "required": [
                        "sources",
                        "install"
                    ]
                },
                "source": {
                    "type": "object",
                    "properties": {
                        "sources": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "install": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        }
                    },
                    "required": [
                        "sources",
                        "install"
                    ]
                },
                "post_install": {
                    "type": "string"
                }
            }
        },
        "macos": {
            "type": "object",
            "properties": {
                "packaged": {
                    "type": "object",
                    "properties": {
                        "packages": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "repositories": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        }
                    },
                    "required": [
                        "packages"
                    ]
                },
                "prebuilt": {
                    "type": "object",
                    "properties": {
                        "sources": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "install": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        }
                    },
                    "required": [
                        "sources",
                        "install"
                    ]
                },
                "source": {
                    "type": "object",
                    "properties": {
                        "sources": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        },
                        "install": {
                            "type": "array",
                            "items": {
                                "type": "string"
                            }
                        }
                    },
                    "required": [
                        "sources",
                        "install"
                    ]
                },
                "post_install": {
                    "type": "string"
                }
            }
        }
    },
    "required": [
        "name"
    ]
}
```

You can use https://toolkit.site/format.html to convert among JSON, YAML and TOML.

# TODO

- [ ] Enable / disable a package by symlinking it into the corresponding
  macos/ubuntu directory
- [ ] Should groups be implemented as a part of filesystem heirarchy or should
  it be a field in the JSON
- [ ] A proof-of-concept for converting JSON to Ansible task