# Result comparison of applied LRP to Brain MRI scans and Covid CT scans

We apply layer-wise relevance propagation to Brain MRI scans and Covid CT scans. Then we compare the results of these. 

## Description
We follow Montavon's [tutorial](<https://git.tu-berlin.de/gmontavon/lrp-tutorial>) and DeepFindr's [repository](<https://github.com/deepfindr/xai-series>) and apply layer wise relevance propagation on a pretrained VGG16 network using two different dataset. The first one, used in DeepFindr's repository is comprised of brain magnetic resonances with different tumour classes, while the second one contains chest computarized tomography scans classified as "Covid" and "Non-Covid". 

The main idea was to find characteristics that helped recognize Covid on CT scans easily.

## Results 
On the brain MRI images, the VGG16 has an accuracy of 0.76 on the test set, while it has a 0.98 accuracy on the Covid set.

Then we perform an exploratory search of the images and find that the Brain MRI images show the tumours marked as positively relevant even when there are other round structures nearby (Upper, left image). Furthermore, when the tumour is not correctly classified, the LRP shows that the network perceives the tumour as positively relevant (Bottom, left image). However, when the tumour is blurred, it can miss it still and misclassify it (Bottom, right image). This was not a common occurence as most of the misclassifications where between tumours. 

![BrainGithub](https://user-images.githubusercontent.com/29287072/158022317-e7ef8ecb-3631-45d2-8a0a-e410701e913d.jpg)

We do the same search for the images on the Covid set. First we have a healthy lung CT classified correctly (Left image) where we can see more negatively relevant features rather than positive ones. To the right, we have a Coivd infected lung classified correctly. In this case we see some circular structures in the lung being detected as positively relevant, but as we do not know so much about Sars-Cov-2 and we are not radiologists, we are unsure of which structures or signs to look at, so we do not venture to say whether the network is focusing on the correct or incorrect features. 

![CovidGithub](https://user-images.githubusercontent.com/29287072/158022729-e9ca2892-3fa0-4ae3-92d3-efd06f3c043b.png)

Finally, we have an image of an infected lung misclassified as healthy. In this case, we see the lungs edges being detected, half being positively relevant and the other half negatively relevant. The trachea is also shown as positively relevant. However, we also see the circular structures seen before, which are positively relevant as well. This seems to contradict what we saw on the figure above to the right. Once again, we do not venture to say whether these structures are actually relevant or not due to lack of knowledge and training on reading these images. 

![image](https://user-images.githubusercontent.com/29287072/158023262-7488b463-6a4e-4918-9c41-4e65bc8bcb82.png)

What we take from this experience is that on the first dataset, we have images being incorrectly classified, but the features that we want the network to learn are being detected, i.e., the tumours. However, on the second dataset, we find contradictory features being used to classify the images. What’s interesting about this is that the brain MRI scans has a worse performance on the test set than the chest CT scans. This leads us to the question whether there is a correlation between the performance of a network and it learning important features. To do so, layer wise relevance propagation is a good tool as it allows us to see which features are being used to classify and which are guiding the network to a different classification. 

This project lead to the M. Sc. Bionics Thesis at Hochschule Rhein Waal, which can be found in this [repository](<https://github.com/martingorosito/Accuracy_and_detected_features>)

### Links
[Montavon, G., Binder, A., Lapuschkin, S., Samek, W., & Muller, KR. (2019). Layer-Wise Relevance Propagation: An Overview.](<https://link.springer.com/chapter/10.1007%2F978-3-030-28954-6_10>)

[Montavon, G. (2019). Tutorial: Implementing Layer Wise Relevance Propagation.](<https://git.tu-berlin.de/gmontavon/lrp-tutorial>)

[DeepFindr. (2021). Layer wise Relevance Propagation with MRI data.](<https://github.com/deepfindr/xai-series>)

[Soares, E., & Angelov, P. (2020). SARS-COV-2 Ct-Scan Dataset. ](<https://www.kaggle.com/plameneduardo/sarscov2-ctscan-dataset/version/2>)

[Bhuvaji, S., Kadam, A., Bhumkar, P., Dedge, S., & Kanchan, S. (2020). Brain Tumor Classification (MRI)](<https://www.kaggle.com/sartajbhuvaji/brain-tumor-classification-mri>)
