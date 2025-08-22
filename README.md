# UPW Tools

This is **very much** a work in progress. We'll be adding more functionality as we go. e.g., fetching secrets from Vault. 

## Dependencies

You'll need [docker](https://docs.docker.com/desktop/setup/install/mac-install/) and tilt installed.

```
brew install tilt
```

## Running

Add this to your profile (./.zshrc or ~/.bashrc), obviously change the paths to match your local setup:

```shell
export LOCAL_UPW_API_PATH=$HOME/Desktop/hmpps/api
export LOCAL_UPW_UI_PATH=$HOME/hmpps/ui
```

Then either open a new terminal or run ``:

```shell
source ~/.zshrc # or source ~/.bashrc
```

Then run tilt:

```shell
tilt up
```

## Services

| Tool       | Location     | Port |
|------------|--------------|------|
| HMPPS Auth | local docker | 8080 |
| UPW API    | local native | 8090 |
| UPW UI     | local native | 3000 |
