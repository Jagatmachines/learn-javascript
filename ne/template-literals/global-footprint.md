# ग्लोबल पदचिह्न

यदि तपाईं मोड्युल विकास गर्दै हुनुहुन्छ, जुन वेब पृष्ठमा चलिरहेको हुन सक्छ, जसले अन्य मोड्युलहरू पनि चलाउँदछ, त्यसपछि तपाईंले चर नाम ओभरल्यापिङको बारेमा सावधान हुनुपर्दछ।

मानौं हामी काउन्टर मोड्युल विकास गर्दैछौं:

```javascript
let myCounter = {
  number: 0,
  plusPlus: function () {
    this.number = this.number + 1;
  },
  isGreaterThanTen: function () {
    return this.number > 10;
  },
};
```

> _**नोट:**_ आन्तरिक अवस्थालाई बाहिरबाट अपरिवर्तनीय बनाउन यो प्रविधि प्रायः बन्द गरेर प्रयोग गरिन्छ।

मोड्युलले अब केवल एक चर नाम लिन्छ - `myCounter`। यदि पृष्ठमा कुनै अन्य मोड्युलले 'नम्बर' वा `isGreaterThanTen` जस्ता नामहरू प्रयोग गर्दछ भने यो पूर्ण रूपमा सुरक्षित छ किनकि हामी एक अर्काको मानहरू ओभरराइड गर्नेछैनौं।
