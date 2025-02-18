# घटनाहरू

प्रोग्रामिंगमा, घटनाहरू प्रणालीमा कार्यहरू वा घटनाहरू हुन् जुन प्रणालीले तपाईंलाई सूचित गर्दछ ताकि तपाईं तिनीहरूलाई प्रतिक्रिया दिन सक्नुहुनेछ। उदाहरणका लागि, जब तपाईं रिसेट बटन क्लिक गर्नुहुन्छ यसले इनपुट खाली गर्दछ।

कुञ्जीपाटीबाट (keyboard) अन्तर्क्रियाहरू जस्तै किप्रेसहरू फेरि जारी गर्नु अघि कुञ्जीको अवस्था समात्न निरन्तर पढ्न आवश्यक छ। अन्य समय-गहन गणनाहरू प्रदर्शन गर्दा तपाईंलाई कुञ्जी प्रेस छुट्न सक्छ। यो केही आदिम मेशिनहरूको इनपुट ह्यान्डलिङ संयन्त्र थियो। अर्को कदम एक लाइन प्रयोग गर्न छ, अर्थात् एक प्रोग्राम जुन समय-समयमा नयाँ घटनाहरूको लागि लाइन जाँच गर्दछ र यसमा प्रतिक्रिया गर्दछ। यो दृष्टिकोणलाई _polling_ भनिन्छ।

यस दृष्टिकोणको मुख्य दोष यो हो कि यसले हरेक समय लाइनमा हेर्नुपर्छ, जब एक घटना ट्रिगर हुन्छ तब व्यवधान उत्पन्न हुन्छ। यसको लागि राम्रो संयन्त्र भनेको घटना घट्दा कोडलाई सूचित गर्नु हो। यो आधुनिक ब्राउजरहरूले हामीलाई विशिष्ट घटनाहरूको लागि _ह्यान्डलरहरूको_ रूपमा प्रकार्यहरू दर्ता गर्न अनुमति दिएर के गर्दछ।

```javascript
<p>Click me to activate the handler.</p>
<p>ह्यान्डलर सक्रिय पार्न मलाई क्लिक गर्नुहोस् ।</p>
<script>
  window.addEventListener("click", () => {
    console.log("clicked");
  });
</script>
```

यहाँ, `एडइभेन्ट लिस्टनर (addEventListener)` लाई `सञ्झ्याल (window)` वस्तु (ब्राउजरद्वारा प्रदान गरिएको बिल्ट-इन वस्तु) मा सम्पूर्ण `सञ्झ्याल` का लागि ह्यान्डलर दर्ता गर्न भनिन्छ। यसको `एडइभेन्ट लिस्टनर` विधिलाई कल गर्दा यसको पहिलो तर्कद्वारा वर्णन गरिएको घटना हुँदा दोस्रो तर्क लाई भनिन्छ।

{% hint style="info" %}

घटना श्रोताहरूलाई तब मात्र बोलाइन्छ जब घटना उनीहरूले दर्ता गरेको वस्तुको सन्दर्भमा हुन्छ।

{% endhint %}

केहि सामान्य HTML घटनाहरू उल्लेख गरिएका छन्।

| Event         | Description                                               |
| ------------- | --------------------------------------------------------- |
| `onchange`    | When the user changes or modifies the value of form input |
| `onclick`     | When the user clicks on the element                       |
| `onmouseover` | When cursor of the mouse comes over the element           |
| `onmouseout`  | When cursor of the mouse comes leaves the element         |
| `onkeydown`   | When the user press and then releases the key             |
| `onload`      | When the browser has finished the loading                 |

| घटना          | विवरण                                                       |
| ------------- | ----------------------------------------------------------- |
| `onchange`    | जब प्रयोगकर्ताले फारम आगतको मान परिवर्तन वा परिमार्जन गर्दछ |
| `onclick`     | जब प्रयोगकर्ताले तत्वमा क्लिक गर्दछ                         |
| `onmouseover` | जब माउसको कर्सर तत्वमाथि आउँछ                               |
| `onmouseout`  | जब माउसको कर्सर आउँछ तत्व छोड्छ                             |
| `onkeydown`   | जब प्रयोगकर्ताले प्रेस गर्दछ र त्यसपछि कुञ्जी जारी गर्दछ    |
| `onload`      | जब ब्राउजरले लोडिङ समाप्त गरेको छ                           |


नोड्समा दर्ता गरिएका ह्यान्डलरहरूले पनि बच्चाहरूबाट घटनाहरू प्राप्त गर्न सक्छन। उदाहरणका लागि, यदि अनुच्छेद भित्रको बटन क्लिक गरिएको छ भने, अनुच्छेदमा दर्ता गरिएका ह्यान्डलरहरूले पनि क्लिक घटना प्राप्त गर्नेछन्। दुबैमा ह्यान्डलरहरूको उपस्थितिको मामलामा, तलको एक पहिले जान्छ। यो घटनालाई सुरुआत नोडदेखि यसको मूल नोडसम्म र कागजातको मूलमा बाहिरी रूपमा प्रचार गर्न भनिएको छ।

इभेन्ट ह्यान्डलरले ह्यान्डलरहरूलाई घटना प्राप्त गर्नबाट रोक्नका लागि घटना वस्तुमा `stopPropagation` विधिलाई कल गर्न सक्दछ। यो मामलाहरूमा उपयोगी छ जस्तै, तपाइँसँग क्लिक गर्न योग्य तत्व भित्र एक बटन छ र तपाईं बटन क्लिकबाट बाह्य तत्वको क्लिक योग्य व्यवहार ट्रिगर गर्न चाहनुहुन्न।

```javascript
<p>A paragraph with a <button>button</button>.</p>
<script>
  let para = document.querySelector("p"),
      button = document.querySelector("button");
  para.addEventListener("mousedown", () => {
    console.log("Paragraph handler.");
  });
  button.addEventListener("mousedown", event => {
    console.log("Button handler.");
    event.stopPropagation();
  });
</script>
```

यहाँ, "_`माउसडाउन`_" ह्यान्डलरहरू अनुच्छेद र बटन दुवैद्वारा दर्ता गरिन्छ। बटन क्लिक गरेपछि, बटनको लागि ह्यान्डलरले `स्टपप्रोपेगेसन` कल गर्दछ, जसले अनुच्छेदमा ह्यान्डलरलाई चल्नबाट रोक्नेछ।

घटनाहरू पूर्वनिर्धारित व्यवहार हुन सक्छन्। उदाहरणका लागि, लिङ्कहरू क्लिक मा लिङ्कको लक्ष्यमा नेभिगेट गर्नुहोस्, तपाईं तल तीर क्लिक गरेपछि पृष्ठको तल नेभिगेट गर्नुहुन्छ, र यति मा। यी पूर्वनिर्धारित व्यवहारहरू घटना वस्तुमा `preventDefault` विधिकल गरेर रोक्न सकिन्छ।

```javascript
<a href="https://developer.mozilla.org/">MDN</a>
<script>
  let link = document.querySelector("a");
  link.addEventListener("click", event => {
    console.log("Nope.");
    event.preventDefault();
  });
</script>
```

यहाँ, क्लिक मा लिङ्क को पूर्वनिर्धारित व्यवहार रोकिन्छ, अर्थात् लिङ्क 'लक्ष्य तिर नेभिगेट।
