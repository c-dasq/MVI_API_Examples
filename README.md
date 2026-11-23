# MVI API training notebooks

Simple Jupyter notebooks for learning the IBM Maximo Visual Inspection (MVI) REST API

Each notebook demonstrates **one operation**, and runs on its own; it does not import code from other notebooks.

## Requirements

- Python 3.9 or newer
- A running MVI instance with a valid API URL and API key
- An available dataset, file, or deployed model for examples that need one

Install the packages:

```bash
python -m pip install -r requirements.txt
jupyter lab
```

Open a notebook from `notebooks/`, fill in the variables in its code cell, and run the cell:

```python
API_URL = ""  # Example: https://your-server/api
API_KEY = ""
VERIFY_SSL = False # Set to True if you want to verify SSL certificates
```

`API_URL` **must include `/api`**. MVI API authentication uses an `X-Auth-Token` header containing the API key. The first notebook checks access with a GET request; it does not call a username/password login endpoint. 

`VERIFY_SSL = False` is used in these training examples to support self-signed certificates. This skips TLS certificate verification, so use it **only in a trusted training environment**. Set it to `True` when your server has a trusted SSL certificate!!!

Some notebooks also need `DATASET_ID`, `FILE_ID`, `MODEL_ID`, or a local image filename. Dataset and model IDs can be found in the URL for that object in the MVI UI. The same rule applies to project IDs when used in future examples; those are also kept as editable variables.

## Notebooks

| Notebook                                                                       | What it does                                                                                                  |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- |
| [`01_authenticate.ipynb`](notebooks/01_authenticate.ipynb)                     | Check that the API key can access MVI                                                                         |
| [`02_list_datasets.ipynb`](notebooks/02_list_datasets.ipynb)                   | Get the datasets available to the API key                                                                     |
| [`03_get_dataset.ipynb`](notebooks/03_get_dataset.ipynb)                       | Show information about one dataset                                                                            |
| [`04_create_dataset.ipynb`](notebooks/04_create_dataset.ipynb)                 | Create a new empty dataset                                                                                    |
| [`05_list_dataset_files.ipynb`](notebooks/05_list_dataset_files.ipynb)         | List the files in one dataset                                                                                 |
| [`06_get_file_metadata.ipynb`](notebooks/06_get_file_metadata.ipynb)           | Read user metadata for one dataset file                                                                       |
| [`07_set_file_metadata.ipynb`](notebooks/07_set_file_metadata.ipynb)           | Add one metadata field to a file                                                                              |
| [`08_download_image.ipynb`](notebooks/08_download_image.ipynb)                 | Download a dataset file to your computer                                                                      |
| [`09_upload_image.ipynb`](notebooks/09_upload_image.ipynb)                     | Upload a local image without labels                                                                           |
| [`10_list_models.ipynb`](notebooks/10_list_models.ipynb)                       | List the deployed inference APIs                                                                              |
| [`11_infer_image.ipynb`](notebooks/11_infer_image.ipynb)                       | Send a local image to a deployed model and print its response                                                 |
| [`12_show_inference_results.ipynb`](notebooks/12_show_inference_results.ipynb) | Run inference and draw detected boxes on the image                                                            |
| [`13_infer_image_url.ipynb`](notebooks/13_infer_image_url.ipynb)               | Send a public image URL to a deployed model                                                                   |
| [`14_save_inference_json.ipynb`](notebooks/14_save_inference_json.ipynb)       | Run inference and save the response as a JSON file                                                            |
| [`15_list_object_labels.ipynb`](notebooks/15_list_object_labels.ipynb)         | List the object labels defined for a dataset                                                                  |
| [`16_upload_file_labels.ipynb`](notebooks/16_upload_file_labels.ipynb)         | Add example bounding-box labels to a dataset file                                                             |
| [`17_clone_dataset.ipynb`](notebooks/17_clone_dataset.ipynb)                   | Create a copy of an existing dataset                                                                          |
| [`18_list_file_labels.ipynb`](notebooks/18_list_file_labels.ipynb)             | Read labels attached to a dataset file                                                                        |
| [`19_infer_video_frame.ipynb`](notebooks/19_infer_video_frame.ipynb)           | Send the first frame of a video to a deployed model                                                           |
| [`20_copy_one_file.ipynb`](notebooks/20_copy_one_file.ipynb)                   | Copy the content of one file into another dataset                                                             |
| [`21_read_polygons.ipynb`](notebooks/21_read_polygons.ipynb)                   | Run image inference with `containPolygon=true`, print polygon coordinates, and draw the polygons on the image |

## Suggested learning order

Start with `01`, `02`, `03`, and `05`. Then try `10`, `11`, `12`, and `14`. Then use `21` to read and display segmentation polygons returned by MVI. 

Use dataset creation, upload, labels, metadata, and cloning after you understand the read-only examples.

## Notes

- `04`, `07`, `09`, `16`, `17`, and `20` change data or create new resources on MVI.
- `08` and `14` write local files.
- `12` draws boxes when the model returns `classified` entries with box coordinates; classification models HAVE NO boxes.
- `19` requires OpenCV and sends only the first video frame.
- `20` does not copy existing labels or metadata.
- `21` sends a local image to `POST /dlapis/{MODEL_ID}` with `containPolygon=true` and reads polygon coordinates from the `classified` results. It requires a deployed model that returns polygons.
- `13` needs a public URL accessible from the MVI server.
- Inference requires a **deployed model ID**, not a training model ID.
- API fields can vary by deployed model and server version.

## Sources

- [IBM MVI 8.6 REST API](https://public.dhe.ibm.com/systems/power/docs/powerai/api860.html)
- [IBM API key tokens](https://www.ibm.com/docs/en/masv-and-l/maximo-vi/cd?topic=apis-api-key-tokens)

These examples are adapted and simplified from the sample notebooks supplied for this project.

### Disclaimer

This repository is an independent, community-driven project created for educational and demonstration purposes to help developers understand and interact with the Maximo Visual Inspection (MVI) API.

It is provided **"AS IS"**, without warranties of any kind or any commitment to provide support, maintenance, or updates.

**This project is not affiliated with, endorsed by, sponsored by, or officially supported by IBM, Maximo, or Maximo Visual Inspection.** 

All product names, trademarks, and registered trademarks are the property of their respective owners.
