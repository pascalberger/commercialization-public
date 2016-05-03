---
author: joshbax-msft
title: Windows Certification Newsletter - January 2, 2013
description: Windows Certification Newsletter - January 2, 2013
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 4d7ab342-5960-48e1-b529-3487cc328f23
---

# Windows Certification Newsletter - January 2, 2013


**New Windows Hardware Certification blog!**

The Windows Certification Newsletter has been replaced by the [Windows Hardware Certification blog](http://blogs.msdn.com/b/windows_hardware_certification/). Go to the blog for the updates and info you’re used to seeing in the newsletter. Subscribe today!

## In this issue


[UEFI POST TIME requirement relaxed for some all-in-one systems](#posttime)

[Some HCK 2.0 errata extended, some set to expire](#hckerrata)

[WLK 1.6 active errata extended into 2015](#wlkerrata)

[Windows Touch Test Lab closed for Chinese New Year](#wttl)

[UEFI submission review processes changed](#review)

## <a href="" id="posttime"></a>UEFI POST TIME requirement relaxed for some all-in-one systems


Based on industry feedback, we're relaxing the UEFI POST TIME requirement to enable large storage capacity in all-in-one systems.

Conditions:

-   PCs must be an all-in-one system with integrated displays.

-   Systems that have 3 TB or greater capacity must POST in 10 seconds or less.

-   Systems shipping after Jan 1, 2014, must meet the requirements published on [MSDN](http://msdn.microsoft.com/).

This delayed enforcement erratum begins April 15, 2013, when the [UEFI requirement Erratum 478 relaxation](http://msdn.microsoft.com/windows/hardware/jj679343.aspx) expires, and ends in October 2014.

To take advantage of this new delayed enforcement, Include ID 1250 in your README file starting April 15, 2013.

## <a href="" id="hckerrata"></a>Some HCK 2.0 errata extended, some set to expire


We've updated all active errata filters for [Hardware Certification Kit (HCK) 2.0](http://msdn.microsoft.com/windows/hardware/hh852359). All active errata that weren't fixed have been extended until March 1, 2013. We'll reevaluate active errata by March 1 and either extend or retire it, depending on whether we made fixes to the test kit. We didn't extend the errata that was already set to expired on January 1, 2013.

You can [check the status of all errata](https://sysdev.microsoft.com/Hardware/ec/) on the [Hardware Dashboard](https://sysdev.microsoft.com/hardware/member/). To narrow down the list, use the filters to view only active, expired, or expiring within 30 days. You can also search by ID and title.

Any extension date shouldn't be considered an indication of any retirement date.

## <a href="" id="wlkerrata"></a>WLK 1.6 active errata extended into 2015


We have updated all active errata filters for the [Windows Logo Kit (WLK) 1.6](http://msdn.microsoft.com/windows/hardware/gg487530.aspx) test kit. All errata that were fixed in the kit were expired. All active errata that weren't fixed have been extended until December 1, 2015. (This extension date shouldn't be considered an indication of the kit's retirement date.)

You can [check the status of all errata](https://sysdev.microsoft.com/Hardware/ec/) on the [Hardware Dashboard](https://sysdev.microsoft.com/hardware/member/). To narrow down the list, use the filters to view only active, expired, or expiring within 30 days. You can also search by ID and title.

## <a href="" id="wttl"></a>Windows Touch Test Lab closed for Chinese New Year


We'd like to remind our partners that [Windows Touch Test Lab](http://msdn.microsoft.com/library/windows/hardware/hh872970) will be closed from February 9–17 for Chinese New Year. There will be no device delivery or submission processing during those 9 days.

Partners who want to ensure device certification prior to the holiday should:

-   Email the lab at tab-ext@microsoft.com with submission ID and stack-up details.

-   Submit physical hardware to the lab no later than January 31, 2013.

Submissions made or devices delivered after January 31 might not be processed before the holiday. We also expect submission volume to be heavy, so plan for a 5–10 business day turnaround, in addition to the holiday break.

## <a href="" id="review"></a>UEFI submission review processes changed


UEFI submissions will no longer go through an automated signing process. Instead, we'll review them manually twice a week. You can expect your submission to be processed in about 5 business days. To avoid delays, please follow the guidelines posted on the [UEFI submission page](https://sysdev.microsoft.com/Hardware/member/SubmissionWizard/CreateUefiSubmission.aspx) on the [Hardware Dashboard](https://sysdev.microsoft.com/hardware/member/). Remember when submitting to the [UEFI signing portal](http://msdn.microsoft.com/library/windows/desktop/hh973604) to:

-   Provide descriptive info when submitting content.

-   Submit only product-quality code.

-   Ensure that your code doesn't execute untrusted code.

## Related topics


[Hardware Dev Center](http://msdn.microsoft.com/en-US/windows/hardware/)

[Windows hardware development kits and tools](http://msdn.microsoft.com/windows/hardware/bg127147)

[Windows hardware development samples](http://code.msdn.microsoft.com/windowshardware/)

[Windows Hardware Certification](http://msdn.microsoft.com/en-US/windows/hardware/gg463010)

[Newsletter archive](windows-certification-newsletter-archive.md)

[Your dashboard](https://sysdev.microsoft.com/hardware/member/)

[Getting started](http://msdn.microsoft.com/library/windows/hardware/gg507680/)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20Windows%20Certification%20Newsletter%20-%20January%202,%202013%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




