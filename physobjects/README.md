 PhysObjects Dataset
===================
PhysObjects is a dataset of object physical concept annotations for EgoObjects. We only provide physical concept annotations, not the original image data or metadata annotations.

## EgoObjects ##
Go to https://ai.facebook.com/datasets/egoobjects-downloads/ for image data (`images.zip`) and metadata annotations (`ego_objects_challenge_train.json`, `ego_objects_challenge_test.json`) for the EgoObjects challenge version dataset. We use both train and test metadata annotations from EgoObjects. After loading a metadata annotation `.json` file as a Python dictionary named `data`, the list of object bounding box annotations can be found at `data["annotations"]`. Each bounding box annotation in this list is a dictionary, which has an attribute `id` that we refer to as the annotation ID. It also has an attribute `instance_id`, which identifies which object instance the annotation is for.

## Object Instance ID Splits ##
We provide lists of which object instance IDs we assign to each training split in the folder `instance_ids`. It contains `.json` files for each split, which each consists of the list of values of `instance_id` for that split.

## Concept Annotation Format ##
Concept annotations are provided as .csv files, which can be found at `annotations/[annotation_type]/[concept]/[split].csv`, where `[annotation_type]` is either `automated` or `crowdsourced`, `[concept]` is one of ten physical concepts, and `[split]` is either `train`, `valid`, or `test`. Note that while concept annotations are provided at the annotation ID/bounding box level, it may be desired to treat an annotation at the object instance level, and apply the annotation to other bounding boxes with the same `instance_id`.

### Crowd-Sourced Concept Annotations ###
For crowd-sourced annotations, we collect annotations from 3 crowd-workers per example. Here, we provide all annotations from each crowd-worker, without filtering for annotator agreement or label values. In the evaluations in our paper, we only evaluate on examples with majority agreement across annotators, and for continuous concepts, we only evaluate on examples with definite preference labels (`left` or `right`).

### Continuous Concepts ###
For the 5 continuous concepts (`mass`, `fragility`, `deformability`, `density`, `liquid_capacity`), annotations consist of preference pairs. Each annotation record consists of the following values:
- **property**: the physical concept the annotation is for
- **annotation_id_0**: the first object bounding box annotation ID
- **annotation_id_1**: the second object bounding box annotation ID
- **response**: the preference annotation label. `left` indicates that the object from `annotation_id_0` has the higher concept value, while `right` indicates that the object from `annotation_id_1` has the higher concept value. `equal` indicates the two objects have roughly equal values, and `unclear` indicates that the relationship is unclear.

### Categorical Concepts ###
For the 5 categorical concepts (`material`, `transparency`, `contents`, `can_contain_liquid`, `is_sealed`), annotations consist of labels for individual image bounding boxes. Each annotation record consists of the following values:
- **property**: the physical concept the annotation is for
- **annotation_id_0**: the object bounding box annotation ID
- **response**: a text label for the annotation

### Held-Out Concepts ###
Our two held-out concepts are `density` and `liquid_capacity`. For these concepts, we only included crowd-sourced test data.
