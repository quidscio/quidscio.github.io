---
layout: default
title:  "Western Loudoun Home Internet - Snooze, Starve, or Spend"
date: 2022-12-11 
categories: internet
---

The FCC invites feedback to broadbandmap.fcc.gov ISP services claims. This comparison of broadband providers in Hillsboro, VA shows the service address in question is poorly served for the purposes of remote work where the primary need is day-long connectivity by Google Meet and Zoom. A rural fixed wireless provider is the sole option fitting requirements for a hefty $309/month. Two cellular options fail due to speed, caps after a few days of usage, or both. The one interesting satellite provider isn't actually available. In short, the residential address in question does not have sufficient broadband access to support professional and educational needs except at a very high price.  

Tested services include T-Mobile 5G Home Internet, Verizon Jetpack LTE, and All Points Broadband Wireless. Starlink has not been available for 19 months, having been applied for May 2021. Testing occurred April to December 2022. All graphs show at least one-week of data displayed by hour of day. Data collected via speedtest.net CLI executed via cron three times per hour; 0:05, 0:25, 0:45. ISP determined by detected IP address.  

FCCs data via broadbandmap.fcc.gov cites five providers for the test address. Table 1 shows these providers with the addition of Verizon LTE Jetpack. 

Table 1: broadbandmap.fcc.gov providers and claimed speeds with Verizon added by author 

| Provider             | Technology                  | FCC Claimed Down (Mpbs) | FCC Claimed Up (Mpbs) | Author's Comments                                                                            |
|----------------------|-----------------------------|-------------------------|-----------------------|----------------------------------------------------------------------------------------------|
| Hughes               | GSO Satellite               | 25                      | 3                     | Not tested                                                                                   |
| Starlink             | NGSO Satellite              | 100                     | 10                    | Not actually available                                                                       |
| T-Mobile             | 5G Licensed Fixed Wireless  | 25                      | 3                     | Tested, does not meet claims, capped Cap and minimum speeds render useless for work purposes |
| Viasat               | GSO Satellite               | 30                      | 3                     | Not tested                                                                                   |
| All Points Broadband | Unlicensed Fixed Wireless   | 10                      | 1                     | Tested, exceed claims Expensive $309/month Usable for work purposes                          |
| Verizon              | LTE Licensed Fixed Wireless | n/a                     | n/a                   | Tested, capped Cap renders useless for work purposes                                         |


T-Mobile delivers highly variable speeds heavily influenced by time-of-day. Day and evening download speeds often fall below 1 Mbps with maximum values at 100 Mbps or better during post-midnight hours. Speed checks using a 5G T-Mobile phone during the same hours show downloads in the 40+ Mbps range indicating the slow home internet speeds are throttling induced. Calls to customer support produced hope but no results. 

Verizon's equivalent JetPack service delivers much more consistent download and upload speeds where download is also heavily influenced by hour of day. Download during afternoon and evening hours rarely falls below 15 Mbps. Upload consistently runs 10-20 Mbps depending on hour of day. 

All Points Broadband provides a wireless service which is the default choice for the area. Download consistently runs 10-14 Mbps while upload runs 3-5 Mbps. A $100/month premium raises download speeds to 25 Mbps which is fairly consistently greater than for former 10 Mbps performance cap. 

Overall, Verizon and All Points Broadband provide reliable service during useful hours of the day. However, Verizon's data cap renders the service insufficient for daily video conferencing. T-Mobile falls to kilobit speeds during afternoon and evening hours rendering the home internet service unusable. All Points Broadband is the most reliable option for multi-megabit speeds though peaks are nowhere near Verizon and T-Mobile. 


## T-Mobile 5G Internet

The following chart shows all samples normalized to a 24-hour, daily view. data clearly shows minimum speeds dropping precipitously as the workday begins at 0900 daily. 

![T-Mobile Download Performance imposed on a 24-hour view](/assets/images/Western-Loudoun-Home-Internet/24-Hour-for-T-Mobile.png "24-hour Download Performance")


The following chart limits the vertical scale to a range of -5.0 to 15.0 Mpbs in order to zoom in on minimum speeds in the 1700 to 2200 timeframe. Visually, these speeds drop to Kpbs which is barely useful for email much less conferencing. Not shown are the extremely high number of lost samples due to poor connectivity/reponse. 

![T-Mobile 24-hour Download Performance on restricted vertical scale](/assets/images/Western-Loudoun-Home-Internet/24-Hour-for-T-Mobile_BB.png "24-hour Download Performance")


## Verizon JetPack

Verizon performed significantly better than T-Mobile. However, Verizon also had the lowest data caps which effectively gave only a few days of work utility. Verizon is useful as an occasional backup only. 

![Verizon Download Performance imposed on a 24-hour view](/assets/images/Western-Loudoun-Home-Internet/24-Hour-for-Verizon.png "24-hour Download Performance")



## All Points Broadband

The regional rural wireless provider gives the most reliable service usable for remote work and educational purposes IF one has line of sight to a tower which a number of near-by neighbors do not. The results below show two concentrations of download samples. The first groups just under 10 Mbps showing their $200/month download for that tier very nearly hits that level. The second sample group varies around the 25 Mbps download level depending on time of day. This level represents the $309 tier of service. 


![APB Download Performance imposed on a 24-hour view](/assets/images/Western-Loudoun-Home-Internet/24-Hour-for-APB.png "24-hour Download Performance")



## Starlink

Starlink was ordered in May 2021 with availability projected for late 2022. During 4Q 2022, Starlink announced availability by the end of 2023 and offered a best-effort alternative. Best effort is not sufficient for remote work or educational purposes. 


![Starlink is not yet available](/assets/images/Western-Loudoun-Home-Internet/starlink-only-best-effort.png "24-hour Download Performance")


## Timeline View Across All Providers

The diagram below shows all providers plotted along the same timeline, April to December 2022. The highest and lowest values observed are T-Mobile. See the earliest April samples for T-Mobile. Samples reaching nearly as high but maintaining higher minimums are Verizon. Find Verizon samples in later April to early May. All Points Broadband are those where uploads are tightly grouped about 5 Mpbs. There are sets where the downloads tightly fall around either 13 or 15 Mbps in June and October. In addition, APB's higher 25 Mpbs speeds are seen during August-September and December. These are more scattered but always in the 15-30 Mbps range. 

![Timeline performance for all ISPs](/assets/images/Western-Loudoun-Home-Internet/Timeline-for-ALL.png "Timeline for all ISPs")

