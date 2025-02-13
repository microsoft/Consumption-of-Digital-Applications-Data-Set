# Consumption of Digital Applications Data Set

Digital literacy encompasses a broad range of skills and knowledge related to using digital technologies and information in various contexts, including but not limited to computers, smartphones, and the Internet. Digital literacy plays a fundamental role in several social outcomes, including enabling economic opportunity, social inclusion, and participation in civic activities.
Nonetheless, digital literacy may not be equitably distributed, implying that groups or communities with lower endowments of digital skills may not be able to fully reap the benefits of new technologies.

While closing this gap has been elevated to a major policy goal both in the U.S. and internationally, the measurement of digital literacy still largely relies on crude indicators of technology adoption, such as computing ownership and broadband availability, which suffer from limited samples and insufficient measurement of the depth and variety of usage. Existing comprehensive surveys are designed to offer yardsticks that characterize adoption across the US population and explore only the most essential features of usage, such as whether a household uses email. Similarly, the Pew Research Center (2023) has collected statistics about samples of broadband and smartphone adopters for many years, and it occasionally conduct surveys of usage by adopters in one-off surveys, but rarely the same in-depth survey twice. Designing interventions to close the digital divide requires a more detailed and comprehensive understanding of persisting differences in how individuals use digital technologies and the underlying factors driving these differences.

Our research provides novel data and methodology to measure a proxy of digital literacy--digital usage--for 28,561 US ZIP codes. These metrics are based on telemetry data collected by Microsoft in 2023 during operating system updates for forty million Windows devices across U.S. households that agreed to share these data, using frontier differential privacy practices. Our data assumes that device usage is a proxy for households laptop and desktop usage. The devices are not part of a business contract. This dataset, the most comprehensive measure of US household computing usage ever assembled, surpasses any existing commercial or government survey in its scope and enables granular measurement of the use of digital applications at a massive scale, which, as we show below, captures a different dimension of digital access than traditional metrics based on computing and network infrastructure.  

We construct two indices reflecting distinct digital usage components: the **Media and Information Composite Index** (MCI) and the **Content Creation and Computation Composite Index** (CCI). The MCI captures usage related to media and information consumption and general computing usage across various applications, such as word processing, spreadsheets, and presentations. The CCI captures usage about content creation and specialized digital applications, like image manipulation (e.g., Photoshop) or software developer tools.


## Measuring Digital Literacy
An ideal index for measuring variance in the usage of computing devices across the US population should be constructed generally. It allows the index to be regularly updated and regionally disaggregated and lends itself to longitudinal analysis. A pragmatic index should, however, also find a point that trades off details with satisfying objectives for maintaining anonymity. 

To achieve these conflicting objectives, we construct a measure of usage at the device level and then build weighted averages of these usage measures at the ZIP code level. By aggregating the data through privacy-enhancing technologies, our approach prevents the revelation of any private information.

 We compute, for each device, device-level indices, which are weighted sums of the time spent (in minute, during one month) in the applications corresponding to the two types of digital literacy defined in [1](https://standards.ieee.org/ieee/3527.1/7589/). The weights used in each sum are computed via principal component analysis (PCA). PCA, which has been previously leveraged in the index construction literature, is a natural choice for computing index weights as it assumes that information is captured in the variance of the data features. We publish the average of the device-level indices at a ZIP code level. 

The computations of MCI and CCI are done via a privacy-preserving technique called differential privacy. To compute the differentially private MCI and CCI, we perform a two-step computation.
We start by computing, the differentially private weights of the first component of principal component analysis done at the national level data. After we obtain the dp-weights, we utilize additive noise mechanisms to compute MCI and CCI. 
All Laplace mechanism and PCA implementations utilized in this project were developed by the [OpenDP library](https://github.com/opendp/opendp). The OpenDP library includes a comprehensive set of differential privacy mechanisms, algorithms, and validator. The library is open source, and is maintained and vetted by OpenDP community.

Please refer to [this paper](https://www.nber.org/system/files/working_papers/w32932/w32932.pdf) for a detailed view on index construction and interpretation. 
 
# Data Table

The dataset includes the following fiels:

- ST: is the 2 letter abbreviation of states in the United States https://www.iso.org/obp/ui/#iso:code:3166:US
- ZIP CODE: 5 digit code used to represent geographic area used by the United State Postal Service
- MEDIA AND INFORMATION COMPOSITE INDEX: Weighted average of the MCI of all participating devices, at a ZIP code level. The MCI a weighted sum of the time spent (in minutes,during one month) in MCI applications corresponding as described in Table 1.
- CONTENT CREATION AND COMPUTATIONAL COMPOSITE INDEX: Weighted average of the CCI of all participating devices, at a ZIP code level. The CCI a weighted sum of the time spent (in minutes,during one month) in CCI applications corresponding as described in Table 1.


**Table 1: Description of the activity features used in the indices contruction.**  
  
The table provides a description of monthly activity data features for different application types in Windows, and examples. In addition to the activity features presented in the data, the telemetry system includes device location in ZIP code format.  

| Feature | Description | Applications |  
|---------|-------------|--------------|  
| **Media and Information Composite Index (MCI) features** | | |  
| ss | Minutes of activity in software for visually organizing and analyzing tabular data | Excel, WPS Spreadsheets |  
| dw | Minutes of activity in software for creating written content, such as reports and letters | Adobe Acrobat, Word, Wordpad |  
| em | Minutes of activity in software for sending and receiving electronic messages | Thunderbird, Outlook, Mailbird |  
| pt | Minutes of activity in software for organizing creating visual slideshows | PowerPoint, Canva, Prezi |  
| md | Minutes of activity in software for playing and editing multimedia content | VLC player, Spotify, Windows Media Player |  
| bw | Minutes of activity in software for browsing the internet | Firefox, Chrome, Opera, Edge |  
| cc | Minutes of activity in software for communicating with others remotely | Zoom, Discord, Teams, Telegram |  
| **Content creation and computation composite index (CCI) features** | | |  
| dv | Minutes of activity in software for creating, testing, and debugging code | Unity engine, Visual Studio, IntelliJ IDE |  
| cd | Minutes of activity in software for remote file storage | One Drive, Dropbox, iCloud, Google drive |  
| ut | Minutes of activity in software for system management and optimization | Remote desktop, printer management |  
| sd | Minutes of activity in software that protects systems from cyberthreats | McAfee agent, Norton Security, Bitdefender |  
| ct | Minutes of activity in software for creating and editing digital media | Adobe Photoshop, Virtual DJ, Blender |  


### More About Differential Privacy
Here are links to differential privacy information:
- SmartNoise: https://smartnoise.org, https://github.com/opendifferentialprivacy/smartnoise-core-python, https://github.com/opendifferentialprivacy/smartnoise-sdk 
- OpenDP: https://projects.iq.harvard.edu/opendp and https://github.com/opendifferentialprivacy
- OpenDP.Accuracy: Pitfalls and edge cases. https://github.com/opendifferentialprivacy/smartnoise-samples/blob/master/analysis/accuracy_pitfalls.ipynb
- OpenDP.Privacy preserving statistic al release. https://github.com/opendifferentialprivacy/smartnoise-samples/blob/master/analysis/tutorial_mental_health_in_tech_survey.ipynb 

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft 
trademarks or logos is subject to and must follow 
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
