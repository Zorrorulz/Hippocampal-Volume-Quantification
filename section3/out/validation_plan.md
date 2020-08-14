# Validation Plan

## About Hippocampus Volume for Alzheimer's Progression
Background
Alzheimer's disease (AD) is a progressive neurodegenerative disorder that results in impaired neuronal (brain cell) function and eventually, cell death. AD is the most common cause of dementia. Clinically, it is characterized by memory loss, inability to learn new material, loss of language function, and other manifestations.

For patients exhibiting early symptoms, quantifying disease progression over time can help direct therapy and disease management.

A radiological study via MRI exam is currently one of the most advanced methods to quantify the disease. In particular, the measurement of hippocampal volume has proven useful to diagnose and track progression in several brain disorders, most notably in AD. Studies have shown a reduced volume of the hippocampus in patients with AD.

The hippocampus is a critical structure of the human brain (and the brain of other vertebrates) that plays important roles in the consolidation of information from short-term memory to long-term memory. In other words, the hippocampus is thought to be responsible for memory and learning (that's why we are all here, after all!)

According to Nobis et al., 2019, the volume of hippocampus varies in a population, depending on various parameters, within certain boundaries, and it is possible to identify a "normal" range taking into account age, sex and brain hemisphere.

There is one problem with measuring the volume of the hippocampus using MRI scans, though - namely, the process tends to be quite tedious since every slice of the 3D volume needs to be analyzed, and the shape of the structure needs to be traced. The fact that the hippocampus has a non-uniform shape only makes it more challenging.


## What is the intended use of the product?

The product is intended to be used as software as a medical device for MRI scans of hippocampus stored in DICOM format to assist radiologists
in perform the task of Hippocampus volume quantification faster.

As every slice of a 3D volume needs to be analyzed, and the fact that hippocampus has a non uniform shape, will make volume quantification of Hippocampus a tedious task. The software as a medical device  integrates with the existing clinical workflow and will assist radilogist with additional information to help with Hippocampus volume quantification. This software will run in parallel without impacting the existing clinical systems performance.  

## How was the training data collected?
The training data used is from the Medical Decathlon competition(http://medicaldecathlon.com/).
The dataset is stored as a collection of NIFTI files, with one file per volume, and one file per corresponding segmentation mask. The original images here are T2 MRI scans of the full brain. This dataset is then cropped volumes to only contain the region around the hippocampus to reduce the size of dataset small.

```
From Medical Decathlon website:
The dataset consisted of MRI acquired in 90 healthy adults and 105 adults with a non-affective psychotic disorder
(56 schizophrenia, 32 schizoaffective disorder, and 17 schizophreniform disorder) taken from the
Psychiatric Genotype/Phenotype Project data repository at Vanderbilt University Medical Center (Nashville, TN, USA).
Patients were recruited from the Vanderbilt Psychotic Disorders Program and controls were recruited from the surrounding community.
All participants were assessed with the Structured Clinical Interview for DSM-IV [15].
All subjects were free from significant medical or neurological illness, head injury, and active substance use or dependence.
Structural images were acquired with a 3D T1-weighted MPRAGE sequence (TI/TR/TE, 860/8.0/3.7 ms; 170 sagittal slices;
voxel size, 1.0 mm3). All images were collected on a Philips Achieva scanner (Philips Healthcare, Inc., Best, The Netherlands).
Manual tracing of the head, body, and tail of the hippocampus on images was completed following a previously published protocol [16, 17].

For the purposes of this dataset, the term hippocampus includes the hippocampus proper (CA1-4 and dentate gyrus)
and parts of the subiculum, which together are more often termed the hippocampal formation [18].
The last sliceof the head of the hippocampus was defined as the coronal slice containing the uncal apex.
The resulting 195 labeled images are referred to as hippocampus atlases. Note that the term hippocampus
posterior refers to the union of the body and the tail.

    ---  source reference: https://arxiv.org/pdf/1902.09063.pdf
```

## How did you label your training data?
As per Medical Decathlon website, all data has been labeled and verified by an expert human rater, and with the best effort to mimic the accuracy required for clinical use. Images were collected from multiple medical institutions and reformatted in NIFTI format and double checked for accuracy by two authors.

```
The images were reformatted to NIfTI into a standard anatomical coordinate system, potentially
introducing coordinate transformation errors due to inconsistency in the DICOM coordinate frame.
Each image was manually verified by the second author to rectify these errors. All images
were reformatted to a Right-Anterior-Superior (RAS) coordinate frame, allowing algorithms
to assume that the xyz millimeter coordinates have the same order and direction as the
voxels ijk coordinates. Some images in the Task 1 and Task 2 datasets required a further
rotation by 180 degrees within the axial plan to correct for misformatted headers,
matching the orientation of the remaining images in the task.All non-quantitative
magnitude images were linearly scaled using a robust minmax to the 0–1000 range to avoid
problems with misformatted DICOM headers missing the appropriate scaling factor;
all other images (e.g., CT in Hounsfield units) remained unscaled to preserve their
quantitative nature.
  source reference: https://arxiv.org/pdf/1902.09063.pdf
```

## How was the training performance of the algorithm measured and how is the real-world performance going to be estimated?
Training performance is measured by the following performance metrics:
  * Dice Similarity Coefficient
  * Jaccard Index
  * Sensitivity and
  * Specificity.

  As the gold standard for hippocampus quantification being the manual segmentation method by radiologists, the real world performance
  is going to be estimated based on Dice Similarity between the predicted quantification by the AI model and the segmentation by expert radiologists.
```
Results:
{
  "volume_stats": [
    {
      "filename": "hippocampus_265.nii.gz",
      "dice": 0.9094481742262976,
      "jaccard": 0.8339339339339339,
      "sensitivy": 0.8932132518494693,
      "specificity": 0.9982158282674158
    },
    {
      "filename": "hippocampus_087.nii.gz",
      "dice": 0.9142700629964393,
      "jaccard": 0.8420787083753785,
      "sensitivy": 0.9004585918532506,
      "specificity": 0.9981597244599113
    },
    {
      "filename": "hippocampus_193.nii.gz",
      "dice": 0.9134150873281308,
      "jaccard": 0.8406292749658003,
      "sensitivy": 0.9076809453471196,
      "specificity": 0.99836931903971
    },
    {
      "filename": "hippocampus_095.nii.gz",
      "dice": 0.9056603773584906,
      "jaccard": 0.8275862068965517,
      "sensitivy": 0.8813738441215324,
      "specificity": 0.998184220432687
    },
    {
      "filename": "hippocampus_161.nii.gz",
      "dice": 0.9265235364715295,
      "jaccard": 0.8631055900621118,
      "sensitivy": 0.9346246973365617,
      "specificity": 0.9977943756579277
    },
    {
      "filename": "hippocampus_125.nii.gz",
      "dice": 0.8361918095904796,
      "jaccard": 0.7184962406015037,
      "sensitivy": 0.876375641966251,
      "specificity": 0.9965455992433767
    },
    {
      "filename": "hippocampus_294.nii.gz",
      "dice": 0.8843385058390657,
      "jaccard": 0.7926584456552911,
      "sensitivy": 0.8509852216748769,
      "specificity": 0.9982942217654448
    },
    {
      "filename": "hippocampus_172.nii.gz",
      "dice": 0.9276433121019109,
      "jaccard": 0.8650510810168686,
      "sensitivy": 0.9281162375732858,
      "specificity": 0.9978868192196009
    },
    {
      "filename": "hippocampus_334.nii.gz",
      "dice": 0.7857844099744747,
      "jaccard": 0.6471539456662354,
      "sensitivy": 0.7471994025392084,
      "specificity": 0.9969689426441949
    },
    {
      "filename": "hippocampus_288.nii.gz",
      "dice": 0.923986032769272,
      "jaccard": 0.8587119321018473,
      "sensitivy": 0.8946684005201561,
      "specificity": 0.9989394148995738
    },
    {
      "filename": "hippocampus_390.nii.gz",
      "dice": 0.8749194068343005,
      "jaccard": 0.7776504297994269,
      "sensitivy": 0.8345633456334564,
      "specificity": 0.998438279219927
    },
    {
      "filename": "hippocampus_141.nii.gz",
      "dice": 0.9265223024245789,
      "jaccard": 0.863103448275862,
      "sensitivy": 0.9222549742078113,
      "specificity": 0.9985957388980325
    },
    {
      "filename": "hippocampus_245.nii.gz",
      "dice": 0.8236397748592871,
      "jaccard": 0.7001594896331739,
      "sensitivy": 0.7921804511278195,
      "specificity": 0.9968793515906738
    },
    {
      "filename": "hippocampus_292.nii.gz",
      "dice": 0.9012696041822256,
      "jaccard": 0.8202827623708537,
      "sensitivy": 0.8672032193158954,
      "specificity": 0.9986922434924328
    },
    {
      "filename": "hippocampus_251.nii.gz",
      "dice": 0.8454756380510441,
      "jaccard": 0.7323151125401929,
      "sensitivy": 0.7644755244755245,
      "specificity": 0.9989088204835941
    },
    {
      "filename": "hippocampus_319.nii.gz",
      "dice": 0.8748195504227676,
      "jaccard": 0.7774926686217009,
      "sensitivy": 0.8757225433526011,
      "specificity": 0.9976948457957302
    },
    {
      "filename": "hippocampus_309.nii.gz",
      "dice": 0.8483658297096367,
      "jaccard": 0.7366626065773447,
      "sensitivy": 0.8372093023255814,
      "specificity": 0.9963657004688468
    },
    {
      "filename": "hippocampus_152.nii.gz",
      "dice": 0.9262007028504491,
      "jaccard": 0.8625454545454545,
      "sensitivy": 0.8908362543815723,
      "specificity": 0.9990868662084733
    },
    {
      "filename": "hippocampus_204.nii.gz",
      "dice": 0.9303698558777566,
      "jaccard": 0.8698051948051948,
      "sensitivy": 0.9324747650539505,
      "specificity": 0.998568296411058
    },
    {
      "filename": "hippocampus_097.nii.gz",
      "dice": 0.8893234258897145,
      "jaccard": 0.8007042253521127,
      "sensitivy": 0.8260079912822376,
      "specificity": 0.999415318651335
    },
    {
      "filename": "hippocampus_381.nii.gz",
      "dice": 0.928,
      "jaccard": 0.8656716417910447,
      "sensitivy": 0.9016497461928934,
      "specificity": 0.999007696036844
    },
    {
      "filename": "hippocampus_011.nii.gz",
      "dice": 0.9272542471322782,
      "jaccard": 0.8643746616134271,
      "sensitivy": 0.9239004629629629,
      "specificity": 0.9983472222222223
    },
    {
      "filename": "hippocampus_169.nii.gz",
      "dice": 0.9262608695652174,
      "jaccard": 0.8626498218334953,
      "sensitivy": 0.931444561035327,
      "specificity": 0.9984232038009088
    },
    {
      "filename": "hippocampus_101.nii.gz",
      "dice": 0.9104347826086957,
      "jaccard": 0.8355945730247406,
      "sensitivy": 0.8739565943238731,
      "specificity": 0.9988530675230429
    },
    {
      "filename": "hippocampus_328.nii.gz",
      "dice": 0.9229376777863977,
      "jaccard": 0.8569027611044417,
      "sensitivy": 0.9019459186252211,
      "specificity": 0.9986287914246725
    },
    {
      "filename": "hippocampus_230.nii.gz",
      "dice": 0.9346301020408163,
      "jaccard": 0.8772822508231068,
      "sensitivy": 0.9260663507109005,
      "specificity": 0.9987068237092117
    },
    {
      "filename": "hippocampus_008.nii.gz",
      "dice": 0.9363859864781807,
      "jaccard": 0.8803813926610806,
      "sensitivy": 0.938115763546798,
      "specificity": 0.9985229668256962
    },
    {
      "filename": "hippocampus_001.nii.gz",
      "dice": 0.8994267847837415,
      "jaccard": 0.8172348484848485,
      "sensitivy": 0.8782225237449118,
      "specificity": 0.998433182349087
    },
    {
      "filename": "hippocampus_019.nii.gz",
      "dice": 0.8851841113366193,
      "jaccard": 0.7940182054616385,
      "sensitivy": 0.9097139451728248,
      "specificity": 0.9966065232477446
    },
    {
      "filename": "hippocampus_181.nii.gz",
      "dice": 0.9232037367770298,
      "jaccard": 0.8573615718295483,
      "sensitivy": 0.9100758396533044,
      "specificity": 0.9982734491466123
    },
    {
      "filename": "hippocampus_260.nii.gz",
      "dice": 0.9041141340411414,
      "jaccard": 0.8250075688767787,
      "sensitivy": 0.8798837584759445,
      "specificity": 0.998531330429265
    },
    {
      "filename": "hippocampus_295.nii.gz",
      "dice": 0.8899405083829097,
      "jaccard": 0.8017052375152254,
      "sensitivy": 0.9071113561190739,
      "specificity": 0.9965863223885724
    },
    {
      "filename": "hippocampus_329.nii.gz",
      "dice": 0.8156471077819393,
      "jaccard": 0.6886858749121574,
      "sensitivy": 0.8,
      "specificity": 0.9956191136449122
    },
    {
      "filename": "hippocampus_074.nii.gz",
      "dice": 0.9176074136478517,
      "jaccard": 0.847758405977584,
      "sensitivy": 0.9076666666666666,
      "specificity": 0.9985728903010394
    },
    {
      "filename": "hippocampus_250.nii.gz",
      "dice": 0.9199696279422931,
      "jaccard": 0.8517997750281214,
      "sensitivy": 0.8828329932964151,
      "specificity": 0.9991066898212665
    },
    {
      "filename": "hippocampus_007.nii.gz",
      "dice": 0.9361012956419317,
      "jaccard": 0.8798782175477442,
      "sensitivy": 0.9427639383155397,
      "specificity": 0.9982265328348983
    },
    {
      "filename": "hippocampus_052.nii.gz",
      "dice": 0.9182624941616068,
      "jaccard": 0.8488773747841105,
      "sensitivy": 0.8774174352871169,
      "specificity": 0.9991685246094641
    },
    {
      "filename": "hippocampus_234.nii.gz",
      "dice": 0.8735045461796139,
      "jaccard": 0.7754177286887567,
      "sensitivy": 0.8513681592039801,
      "specificity": 0.9979335047759
    },
    {
      "filename": "hippocampus_033.nii.gz",
      "dice": 0.9147147147147147,
      "jaccard": 0.8428334255672385,
      "sensitivy": 0.8898626935436751,
      "specificity": 0.9985502296102319
    },
    {
      "filename": "hippocampus_340.nii.gz",
      "dice": 0.8845216826376482,
      "jaccard": 0.7929528246942341,
      "sensitivy": 0.8482866043613707,
      "specificity": 0.9984017124509454
    },
    {
      "filename": "hippocampus_145.nii.gz",
      "dice": 0.924897844159504,
      "jaccard": 0.8602883355176933,
      "sensitivy": 0.9281674208144797,
      "specificity": 0.9980614230127849
    },
    {
      "filename": "hippocampus_199.nii.gz",
      "dice": 0.8405491024287223,
      "jaccard": 0.7249544626593807,
      "sensitivy": 0.77431906614786,
      "specificity": 0.9988253614530614
    },
    {
      "filename": "hippocampus_143.nii.gz",
      "dice": 0.8786397449521786,
      "jaccard": 0.7835481425322214,
      "sensitivy": 0.8623279098873592,
      "specificity": 0.9981270643093064
    },
    {
      "filename": "hippocampus_243.nii.gz",
      "dice": 0.889228159457167,
      "jaccard": 0.8005497861942578,
      "sensitivy": 0.8866711772665764,
      "specificity": 0.9976670481556476
    },
    {
      "filename": "hippocampus_358.nii.gz",
      "dice": 0.879543834640057,
      "jaccard": 0.7849872773536896,
      "sensitivy": 0.8548666435746449,
      "specificity": 0.9981704669224691
    },
    {
      "filename": "hippocampus_280.nii.gz",
      "dice": 0.7956817273090764,
      "jaccard": 0.6606905710491368,
      "sensitivy": 0.7615767317259855,
      "specificity": 0.9973210509000329
    },
    {
      "filename": "hippocampus_318.nii.gz",
      "dice": 0.8560109705927167,
      "jaccard": 0.7482685135855088,
      "sensitivy": 0.7989192263936291,
      "specificity": 0.9983922829581994
    },
    {
      "filename": "hippocampus_178.nii.gz",
      "dice": 0.9175696594427245,
      "jaccard": 0.8476939578119413,
      "sensitivy": 0.8736182756079587,
      "specificity": 0.9994098659044693
    },
    {
      "filename": "hippocampus_184.nii.gz",
      "dice": 0.9261443414771132,
      "jaccard": 0.8624476987447699,
      "sensitivy": 0.9148404993065187,
      "specificity": 0.9985197401772257
    },
    {
      "filename": "hippocampus_235.nii.gz",
      "dice": 0.8330626826891848,
      "jaccard": 0.7138881157806847,
      "sensitivy": 0.84375,
      "specificity": 0.996276395173454
    },
    {
      "filename": "hippocampus_180.nii.gz",
      "dice": 0.9285449833395039,
      "jaccard": 0.866620594333103,
      "sensitivy": 0.936519790888723,
      "specificity": 0.9985491086422075
    },
    {
      "filename": "hippocampus_210.nii.gz",
      "dice": 0.9173135335808302,
      "jaccard": 0.8472568578553616,
      "sensitivy": 0.9075125208681135,
      "specificity": 0.9984369152191621
    }
  ],
  "overall": {
    "mean_dice": 0.8946818424512935,
    "mean_jaccard": 0.811494408219883,
    "mean_sensitivity": 0.8765961380703617,
    "mean_specificity": 0.9981588543621249
  },
  "config": {
    "name": "Basic_unet",
    "root_dir": "../data",
    "n_epochs": 10,
    "learning_rate": 0.0002,
    "batch_size": 16,
    "patch_size": 64,
    "test_results_dir": "../out"
  }
}
```
## What data will the algorithm perform well in the real world and what data it might not perform well on?
The algorithm will perform well for MRI scans of hippocampus stored in DICOM format. The algorithm will not perform well on MRI images of other body part scans. The algorithm will not perform well if the co-ordinate system transformation errors occur during the collection of the images.
The algorithm will not perform well if xyz millimeters doesnt have the same order and direction as voxel ijk coordinates.
