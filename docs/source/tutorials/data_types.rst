.. _supported-tasks:

Supported Tasks & Datasets
===============
For Contrastive Learning, this is an example for attack on clip model:
.. code-block:: bash
  cd attacks/image_text
  python attack_encoder.py \
  --lr 2e-4 \
  --epochs 1 \
  --batch_size 128 \
  --results_dir ./output/CLIP_text/stl10_backdoored_encoder/ \
  --shadow_dataset imagenet \
  --pretrained_encoder ../../resources/image_text/output/CLIP_text/clean_encoder/clean_ft_imagenet.pth \
  --encoder_usage_info CLIP \
  --gpu 0 \
  --arch resnet18 \
  --reference_file ../../resources/image_text/reference/CLIP/one.npz \
  --reference_type text \
  --reference_word truck \
  --trigger_file ../../resources/image_text/trigger/trigger_pt_white_185_24.npz \
  --save_id _1234 \
  --seed 1234
and use below command to validate the attack results:
.. code-block:: bash
  cd attacks/image_text
  python compute_zscore.py \
  --gpu 0 \
  --batch_size 64 、\
  --id 1234 \
  --encoder_path ../../resources/image_text/output/CLIP_text/stl10_backdoored_encoder/model_1_tg24_clip_txt_atk_2001.pth \
  --res_file clip_val_txt
this is an example for defense of clip:
.. code-block:: bash
    cd defenses/image_text
    python decree.py \
    --gpu 3 \
    --model_flag backdoor \
    --batch_size 32 \
    --lr 0.5 \
    --seed 1234 \
    --encoder_path ../../resources/image_text/output/CLIP_text/stl10_backdoored_encoder/model_1_tg24_clip_txt_atk_2001.pth \
    --mask_init rand \
    --id 1234 \
    --encoder_usage_info CLIP \
    --arch resnet50 \
    --result_file resultfinal_cliptxt.txt
For VQA tasks, we supply an example to generate poisoned dataset:
.. code-block:: bash
  cd attacks/vqa/BAGS
  python extract_features.py --feat_id troj_f0
  python compose_dataset.py --feat_id troj_f0 --data_id troj_d0
BackdoorMBTI supports a wide range of tasks across different modalities. The following table summarizes the supported tasks and their respective modalities:

.. list-table:: Supported Tasks
   :header-rows: 1
   :widths: 50 50

   * - Task
     - Modality
   * - Object Classification
     - Image
   * - Traffic Sign Recognition
     - Image
   * - Facial Recognition
     - Image
   * - Sentiment Analysis
     - Text
   * - Topic Classification
     - Text
   * - Speech Command Recognition
     - Audio
   * - Music Genre Classification
     - Audio
   * - Speaker Identification
     - Audio
   * - Video Classification (New)
     - Video
   * - Audiovisual Sentiment Analysis (New)
     - Audiovisual
   * - Visual Question Answering (VQA) (New)
     - Image/Text
   * - Contrastive Learning (New)
     - Image/Contrastive
