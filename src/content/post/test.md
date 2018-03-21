## Investigating Ad Transparency Mechanisms in Social Media: A Case Study of Facebook’s Explanations
> Andreou, Athanasios, et al. "Investigating ad transparency mechanisms in social media: A case study of Facebook’s explanations." NDSS, 2018.[[PDF]](http://wp.internetsociety.org/ndss/wp-content/uploads/sites/25/2018/02/ndss2018_10-1_Andreou_paper.pdf)

### What is ad transparency mechanisms in social media？ 

Transparency mechanisms are solutions for many privacy complaints from users and policy makers. Users have little understanding of what data the advertising platforms have about them and why they are shown particular ads. The transparency mechanisms in Facebook are "Why am I seeing this?" botton that provides  users with an explanation of why they were shown a particular ad (ad explanations), and an Ad Preferences Page that provides users with a list of attributes Facebook has inferred about them and how (data explanations). In Twitter, there are similar transparency mechanisms. You can also see "Why am I seeing this?" botton that provides  users with an explanation of why they were shown a particular ad (ad explanations) in Twitter.

### What did this paper do?

This paper mainly did an investigation and analysis of ad explanations, or why users see a certain ad and an investigation of data explanations, or how data is inferred about a user, which is strongly related to the ad transparency mechanisms in Facebook. This paper first introduced how ad platform in facebook works and then evaluate the two transparency mechanisms we introduced before with some properties.

The Ad platform in Facebook
There are three main processes in facebook ad platform: 1) the data inference process; 2) the audience selection process; 3) the user-ad matching process
(1) The data inference process is the process that allows the advertising platform to learn the users’ attributes. It has three parts: (a) the raw user data (the inputs), containing the information the
advertising platform collects about a user either online or offline; (b) the data inference algorithm (the mapping function between inputs and outputs), covering the algorithm the advertising platform uses to translate input user data to targeting attributes;(c) the resulting targeting attributes (the outputs) of each user that advertisers can specify to select different groups of users.

(2) The audience selection process is the interface that allows advertisers to express who should receive their ads. Advertisers create audiences by specifying the set of targeting attributes the audience needs to satisfy. Later, to launch an ad campaign, advertisers also need to specify a bid price and an optimization criterion.
(3) The user-ad matching process takes place whenever someone is eligible to see an ad. It examines all the ad campaigns placed by different advertisers in a particular time interval, their bids, and runs an auction to determine which ads are selected.
pictures!!!


Ad Explanations and the experiments on this transparency mechanism

图（why am I seeing this）
As you can see in the picture, There're attritubutes and potentional here. 
This paper used 5 different properties to evaluate the performance of Ad explanations:
1. Correctness: Every attribute listed was used by the advertiser
2. Personalization: The attributes listed are unique to the individual
3. Completeness: If all relevant attributes are included in the explanation
4. Consistency: Users with the same attributes see the same explanations
5. Determinism: A user would see the same explanation for ads based on the same target attributes

The experiment this paper did to evaluate the ad explanations is using Chrome browser extension to record ads and explanations. The experiment had 35 users' data across 5 months. This experiment also did to evaluate the data explanation. This paper made simple statistics for the explanation(See the following figure). And then, it shows the results of different properties on this experiment.

Data Explanations and the experiments on this transparency mechanism

The data explanations is applied in "Your interests" part as shown in the following picture. The properties here are not the same as those used in the Ad explanation part. There are 3 new properties.
1. Specificity: A data explanation is precise if it shows the precise activities that were used to infer an attribute about a user.
2. Snapshot completeness: A data explanation is snapshot complete if the explanation shows all the inferred attributes about the user that Facebook makes available.
3.Temporal completeness: a temporally complete explanation is one where the platform shows all inferred attributes over a specified period of time.

The results of different properties on this experiment are showed in the following picture.

While the Ad Preferences Page does bring some transparency to the different attributes users can be targeted with,
the provided explanations are incomplete and often vague. Facebook does not provide information about data-brokerprovided attributes in its data explanations or in its ad explanations




