# वस्तुहरू

जाभास्क्रिप्टमा वस्तुहरू **उत्परिवर्तनीय** छन् किनकि हामी सन्दर्भ वस्तुद्वारा इंगित मानहरू परिवर्तन गर्दछौं, यसको सट्टा, जब हामी एक आदिम मान परिवर्तन गर्दछौं हामी यसको सन्दर्भ परिवर्तन गर्दैछौं जुन अब नयाँ मानलाई इंगित गर्दैछ र त्यसैले आदिम **अपरिवर्तनीय** हो। जाभास्क्रिप्टका आदिम प्रकारहरू 'सत्य', 'गलत', संख्याहरू, स्ट्रिङहरू, 'शून्य' र 'अपरिभाषित' हुन्। प्रत्येक अन्य मान एक 'वस्तु' हो। वस्तुहरूले 'गुणनाम' समावेश गर्दछ: 'गुणभ्यालु' जोडी । जाभास्क्रिप्टमा 'वस्तु' सिर्जना गर्ने तीन तरिकाहरू छन्:

1. literal (शाब्दिक)

    ```javascript
    let object = {};
    // Yes, simply a pair of curly braces!
    ```

    > _**नोट:**_ यो **सिफारिस गरिएको** तरिका हो।

2. object-oriented (वस्तु उन्मुख)

    ```javascript
    let object = new Object();
    ```
    > _**नोट:**_ यो लगभग जाभा जस्तै छ।

3.  and using `object.create`

    ```javascript
    let object = Object.create(proto[, propertiesObject]);
    ```

    > _**नोट:**_ यसले निर्दिष्ट प्रोटोटाइप वस्तु र गुणहरूको साथ नयाँ वस्तु सिर्जना गर्दछ।

