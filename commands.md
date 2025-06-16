``` az login```
```az acr login --name <your-acr-name>```


``` docker build -t <acr-name>.azurecr.io/<image-name>:<new-tag> . ```


``` docker push <acr-name>.azurecr.io/<image-name>:<new-tag> ```
