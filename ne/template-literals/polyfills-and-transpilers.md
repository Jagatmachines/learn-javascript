# पोलिफिल र ट्रान्सपाइलरहरू

जाभास्क्रिप्टमा नियमित रूपमा, नयाँ भाषा प्रस्तावहरू प्रस्तुत गरिन्छ, विश्लेषण गरिन्छ, र [https://tc39.github.io/ecma262/](https://tc39.github.io/ecma262/) मा थपिन्छ र त्यसपछि स्पेसिफिकेसनमा समावेश गरिन्छ। ब्राउजरको आधारमा जाभास्क्रिप्ट इन्जिनमा यसलाई कसरी लागू गरिन्छ भन्ने मा भिन्नता हुन सक्छ। कोही-कोहीले ड्राफ्ट प्रस्तावहरू लागू गर्न सक्छन्, जबकि अरूले सम्पूर्ण स्पेसिफिकेसन जारी नभएसम्म पर्खन्छन्। पश्चगामी अनुकूलता मुद्दाहरू नयाँ चीजहरू प्रस्तुत हुँदा उत्पन्न हुन्छन्।

पुरानो ब्राउजरमा आधुनिक कोडसमर्थन गर्न हामी दुई उपकरणहरू प्रयोग गर्दछौं: 'ट्रान्सपाइलर' र 'पोलिफिल'

**ट्रान्सपाइलर**

यो एक प्रोग्राम हो जसले आधुनिक कोडअनुवाद गर्दछ र पुरानो वाक्य संरचना निर्माणहरू प्रयोग गरेर यसलाई पुनर्लेखन गर्दछ, ताकि पुरानो इन्जिनले यसलाई बुझ्न सकोस्। उदाहरणका लागि, "`nullish` कोलेसिङ अपरेटर" '?? ' 2020 मा प्रस्तुत गरिएको थियो, र पुरानो ब्राउजरहरूले यसलाई बुझ्न सक्दैनन्

अब, यो ट्रान्सपाइलरको काम हो कि 'शून्य' कोलेसिंग अपरेटर " '?? ' पुरानो ब्राउजरलाई बुझ्न सकिने

```javascript
// before running the transpiler
height = height ?? 200;

// after running the transpiler
height = height !== undefined && height !== null ? height : 200;
```

{% hint style="info" %}

[बाबेल](https://babeljs.io/) सबैभन्दा प्रमुख ट्रान्सपिलरहरू मध्ये एक हो। विकास प्रक्रियामा, हामी [वेबप्याक](https://webpack.js.org/) वा [पार्सल](https://parceljs.org/) जस्ता निर्माण उपकरणहरू प्रयोग गर्न सक्दछौं।
{% endhint %}

**पोलिफिल**

पुरानो ब्राउजर इन्जिनहरूमा नयाँ कार्यक्षमता उपलब्ध छैन। यस अवस्थामा, नयाँ कार्यक्षमता प्रयोग गर्ने कोडले काम गर्दैन। खाली स्थानहरू भर्न, हामी हराएको कार्यक्षमता थप्छौं जसलाई "`पोलिफिल` भनिन्छ। उदाहरणका लागि, `filter()` विधि ईएस 5 मा पेश गरिएको थियो र केहि पुरानो ब्राउजरहरूमा समर्थित छैन। यो विधिले प्रकार्य स्वीकार गर्दछ र मूल सरणीको मान मात्र भएको सरणी फर्काउँछ जसका लागि प्रकार्यले 'सत्य' फर्काउँछ ।

```javascript
const arr = [1, 2, 3, 4, 5, 6];
const filtered = arr.filter((e) => e % 2 === 0); // filter outs the even number
console.log(filtered);

// [2, 4, 6]
```
फिल्टरको लागि पोलिफिल:

```javascript
Array.prototype.filter = function (callback) {
	// Store the new array
	const result = [];
	for (let i = 0; i < this.length; i++) {
		// call the callback with the current element, index, and context.
		//if it passes the text then add the element in the new array.
		if (callback(this[i], i, this)) {
			result.push(this[i]);
		}
	}
	//return the array
	return result;
};
```

{% hint style="info" %}

[caniuse](https://caniuse.com/) ले विभिन्न ब्राउजर इन्जिनहरू द्वारा समर्थित अद्यावधिक कार्यक्षमता र वाक्य रचना देखाउँदछ।
{% endhint %}
