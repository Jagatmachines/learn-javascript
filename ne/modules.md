# मोड्युलहरू

वास्तविक संसारमा, एक प्रोग्राम नयाँ कार्यक्षमताको आवश्यकताहरूको सामना गर्न व्यवस्थित रूपमा बढ्छ। बढ्दो कोडबेस संरचना र कोड को रखरखाव को साथ अतिरिक्त काम को आवश्यकता छ। यद्यपि यसले भविष्यमा भुक्तानी गर्नेछ, यसलाई बेवास्ता गर्न र प्रोग्राम हरूलाई गहिरो रूपमा पेचिलो हुन अनुमति दिन यो लोभलाग्दो छ। वास्तविकतामा, यसले अनुप्रयोगको जटिलता बढाउँछ, किनकि एक प्रणालीको समग्र समझ निर्माण गर्न बाध्य हुन्छ र अलगावमा कुनै पनि टुक्रा हेर्न गाह्रो हुन्छ। दोस्रो, यसको कार्यक्षमता को उपयोग गर्न को लागी एक अनटैंगलिंग मा अधिक समय लगानी गर्नु पर्छ।

मोड्युलहरू यी समस्याहरूबाट बच्न आउँदछन्। एक 'मोड्युल' ले निर्दिष्ट गर्दछ कि यो कोडको कुन टुक्राहरूमा निर्भर गर्दछ, साथै यसले अन्य मोड्युलहरू प्रयोग गर्नका लागि कुन कार्यक्षमता प्रदान गर्दछ। मोड्युलहरू जुन अन्य मोड्युलमा निर्भर छन् तिनीहरूलाई \_निर्भरताहरू' भनिन्छ। विभिन्न मोड्युल पुस्तकालयहरू मोड्युलहरूमा कोड व्यवस्थित गर्न र मागमा लोड गर्न त्यहाँ छन्।

- AMD - सबैभन्दा पुरानो मोड्युल प्रणाली मध्ये एक हो। सुरुमा यो [require.js](https://reqirirejs.org/) प्रयोग गरियो।
- CommonJS - मोड्युल प्रणाली नोड ट्रान्स सर्भर को लागी सिर्जना गरिएको हो।।
- UMD - मोड्युल प्रणाली जुन AMD र CommonJS सँग उपयुक्त छ।

मोड्युलहरूले एक अर्कालाई लोड गर्न सक्दछन्, र कार्यक्षमता आदानप्रदान गर्न विशेष निर्देशनहरू आयात र निर्यात प्रयोग गर्न सक्दछन्, र एक अर्काको कार्यहरू कल गर्न सक्दछन्।

- `निर्यात (export)` ले लेबलहरू कार्यहरू र चरहरू जुन हालको मोड्युल बाहिरबाट पहुँच योग्य हुनुपर्दछ।
- `आयात (import)` - बाहिर मोड्युलबाट कार्यक्षमता आयात गर्दछ।

मोड्युलमा 'आयात' र 'निर्यात' संयन्त्र हेरौं। हामीसँग `sayHi` प्रकार्य `sayHi.js` फाइलबाट निर्यात गरिएको छ।

```javascript
// 📁 sayHi.js
export const sayHi = (user) => {
	alert(`Hello, ${user}!`);
};
```

'आयात' निर्देशनको सहायताले `main.js` फाइलमा `sayHi` प्रकार्य खपत हुन्छ।

```javascript
// 📁 main.js
import { sayHi } from "./sayHi.js";

alert(sayHi); // function...
sayHi("Kelvin"); // Hello, Kelvin!
```

यहाँ, आयात निर्देशिकाले सापेक्ष पथ आयात गरेर मोड्युल लोड गर्दछ र `sayHi` चर प्रदान गर्दछ।

मोड्युलहरू दुई तरिकामा निर्यात गर्न सकिन्छ: **नाम** र **पूर्वनिर्धारित** । यसबाहेक, नामित निर्यातहरू इनलाइन वा व्यक्तिगत रूपमा तोक्न सकिन्छ।

```javascript
// 📁 person.js

// inlined named exports
export const name = "Kelvin";
export const age = 30;

// at once
const name = "Kelvin";
const age = 30;
export { name, age };
```

{% hint style="warning" %}

एउटा फाइलमा एउटा मात्र पूर्वनिर्धारित 'निर्यात' हुन सक्छ ।
{% endhint %}

<pre class="language-javascript"><code class="lang-javascript">// 📁 message.js
const message = (name, age) => {
<strong>    return `${name} is ${age} years old.`;
</strong>};
export default message;
</code></pre>

निर्यातको प्रकारका आधारमा हामी यसलाई दुई तरिकाले आयात गर्न सक्छौं। नामित निर्यात घुंघराले ब्रेसेस प्रयोग गरेर निर्माण गरिएको छ जबकि, पूर्वनिर्धारित निर्यात हरू छैनन्।

```javascript
import { name, age } from "./person.js"; // named export import
import message from "./message.js"; // default export import
```

मोड्युलहरू निर्दिष्ट गर्दा, हामीले _circular dependency_ बच्नुपर्छ। सर्कुलर निर्भरता एक स्थिति हो जहाँ मोड्युल ए बी मा निर्भर गर्दछ, र बी पनि प्रत्यक्ष वा अप्रत्यक्ष रूपमा ए मा निर्भर गर्दछ।
