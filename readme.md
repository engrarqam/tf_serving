To start docker container
==========================
```
docker run -it -v C:\48_tf_serving:/48_tf_serving -p 8501:8501 --entrypoint /bin/bash tensorflow/serving
```

To serve only latest model
===========================
```
tensorflow_model_server --rest_api_port=8501 --model_name=email_model --model_base_path=/48_tf_serving/saved_models/
```

To serve models using model config file
========================================
```
tensorflow_model_server --rest_api_port=8501  --allow_version_labels_for_unavailable_models --model_config_file=/48_tf_serving/models.config.c
```


Postman commands
=================

models.config.a => To call for all
```
http://localhost:8501/v1/models/email_model:predict
```

models.config.b => only for specific versions versions
```
http://localhost:8501/v1/models/email_model/versions/2:predict
http://localhost:8501/v1/models/email_model/versions/3:predict

```

models.config.c => To call by versions
```
http://localhost:8501/v1/models/email_model/versions/2:predict
```

models.config.c => To call by labels
```
http://localhost:8501/v1/models/email_model/labels/beta:predict
```

Body: raw
```
{
    "instances": [
        "Let's meet for dinner tomorrow",
        "You are awarded a SiPix Digital Camera! call 09061221061 from landline. Delivery within 28days. T Cs Box177"
    ]
}
```

TF Serving Installation Instructions & Config File Help
=======================================================

https://www.tensorflow.org/tfx/serving/docker
https://www.tensorflow.org/tfx/serving/serving_config
