---
layout: post
title: A Basic Understanding of Satellite Imagery for Machine Learning Practitioners
featured: true
image: assets/images/nasa-yZygONrUBe8-unsplash.jpeg
author: thanakorn
categories: [ data science ]
---

***Earth Observation*** technology has been around for almost a century. The first satellite image of the world was taken in 1959 by the U.S. Explorer 6([Wikipedia](https://en.wikipedia.org/wiki/Satellite_imagery)) and the technology has been continuously developing since then. However, in the early days, satellite imagery was used only by a small group of people and organizations due to the difficulty of access. It's not until the past few decades that satellite images started to gain popularity when NASA and European Space Agency made the data from several satellites such as [MODIS](https://modis.gsfc.nasa.gov/), [Landsat](https://landsat.gsfc.nasa.gov/), and [Sentinel](https://www.esa.int/Applications/Observing_the_Earth/Copernicus/Overview4) freely available.

# Characters of Satellite Imagery  

Satellite images have very different characters from ordinary images that we are all familiar with. The key differences between them are as follow:

1. **Number of Channels**  
    An ordinary image has 3 channels representing an intensity of each mother colors: Red, Green, and Blue. Satellite imagery, on the other hand, can have 6 - 12 channels depending on the satellite taking it. What are those extra channels? The extra channels are reflectances of the signals from different wavelengths. In fact, they are all quite similar in concept to the RGB channels except that these signals are not visible to human eyes. The popular type of signals that are usually found in satellite images are infrared(IR), near-infrared(NIR), and shortwave-infra(SWIR). The reason that these signals are chosen is because they can give very useful information about the earth surface due to their properties. For instance, the near-infrared signal is very [sensitive to chlorophyll](https://science.nasa.gov/ems/08_nearinfraredwaves) so it can be used to indicate which geographical area is vegetation.

2. **Image Size**  
    Another key difference between satellite and normal image is the size of the image. Normally when data scientists perform data analysis or machine learning on image data, those images are in the width and height of a few hundred pixels at most. In contrast, satellite images resolution ranges from 5000x5000 to 10000x10000. That's 100 - 400 times larger in terms of the number of pixels and please don't forget that it has at least twice more channels. This means you have to deal with an immensely larger size of data.

3. **Resolution Difference between Channels**  
    Another character of a satellite imagery which is not found in an ordinary image is that channels have different resolution. As mentioned earlier, a satellite image is made of images where each comes from a signal of a different wavelength. The sensors that are used to acquire these images have different spatial resolutions. The sensors that are used to acquire these images have different spatial resolutions. Therefore, an image taken from a satellite, despite being in the same geographical location, has various resolutions.

These 3 properties make working with satellite imagery requires a different approach from a standard RGB image both in terms of data processing, method of analysis, and algorithms.

# Challenges of working with Satellite Imagery

In the previous section, we've discussed the unique characters of satellite imagery. In this part, we're going to discuss some challenges that data scientists have to deal with while working with this type of data.

1. **Image Splitting**  

    It is practically impossible to use an original image while working with satellite imagery because of its huge dimensions. The most common method to deal with this is to split images into several patches. However, splitting images could affect the performance of your algorithm. For example, if you are building an object detection model, an object of interest may be divided into pieces which make the detection more difficult or even impossible.

    
    |![](/assets/images/sat_img_split.jpeg)| 
    |:--:| 
    | <sup>Object of interest, the ship, get splitted into pieces(Image from [spaceflightnow.com](https://spaceflightnow.com/2021/03/29/remote-sensing-companies-share-satellite-views-of-ship-stuck-in-suez-canal/)).<sup> |

2. **Cloud** 
   
    Satellite images are taken hundreds of km above the earth. This means atmospheric conditions can interfere with the process of data collations. When clouds appear on an image, the measurements of those particular areas are extremely noisy. The easiest way to circumvent this issue is to not use data from those cloudy pixels. However, if your areas of interest happen to be in those pixels this may not be an option. In this scenario, you will need other solutions such as using an image from a different time or replacing cloudy pixels with some values.

    |![](/assets/images/sentinel2_cloud.jpeg)| 
    |:--:| 
    | <sup>A part of the image is covered by cloud(Image from [eox.at](https://eox.at/2017/03/sentinel-2-cloudless/)).<sup> |

3. **Lack of Ground Truth**  

    Most machine learning works require ground truth and the importance of labeled data is well-recognized among machine learning practitioners. Regularly, the ground truth is generated by data labellers who have a decent understanding about the problem. Unlike working with standard images where data labelers can be trained to understand the problem in a short period of time, people who can effectively label satellite images tend to be specialists who either are hard to find or uninterested to do tedious works like data labeling. So, acquiring more ground truth isn't a very practical method. One option to overcome this issue is to use a public dataset if you can find one that is close enough to your problem. If that's not the case, you may need to change your approach from supervised learning to unsupervised or semi-supervised learning.

    |![](/assets/images/sat_img_gt.jpeg)| 
    |:--:| 
    | <sup>Sample ground truth for building ML model for satellite images(Image from [gsittechnology.com](https://www.gsitechnology.com/Beginners-Guide-to-Segmentation-in-Satellite-Images)).<sup> |

# Conclusion

Working with satellite imagery is very different from ordinary images due to the data collection method, types of sensors, the meaning of information, and the amount of data. To use satellite images effectively, data scientists have to understand these differences so they can choose the correct approach to analyze, understand, and model the data to solve their problems.

