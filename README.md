# Ghazal.htmal
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8" />
<title>ग़ज़लें - Deepak mahapatre</title>
<style>
  body {
    font-family: "Mangal", "Noto Sans Devanagari", Arial, sans-serif;
    line-height: 1.6;
    background-color: #f0f8ff;
    padding: 20px;
  }
  h1 {
    text-align: center;
    margin-bottom: 30px;
    color: #00796b;
  }
  #ghazal-text {
    background: #e0f7fa;
    border-radius: 8px;
    padding: 15px 20px;
    box-shadow: 0 0 10px #b2ebf2;
    white-space: pre-line;
    margin-top: 20px;
  }
  label, select, button {
    font-size: 16px;
    margin-right: 10px;
  }
</style>
</head>
<body>

<h1>ग़ज़लें - Deepak mahapatre</h1>

<label for="ghazal-select">ग़ज़ल चुनें:</label>
<select id="ghazal-select">
  <option value="">-- चुनें --</option>
</select>
<button onclick="showGhazal()">पढ़ें</button>

<div id="ghazal-text"></div>

<script>
  // ग़ज़लें ऑब्जेक्ट, हर ग़ज़ल की पूरी कविता (बहुत लाइनें)
  const ghazals = {
    paseena: `किसी का दर्द केवल पूछने से कम नहीं होता,
मेरे यारों नमक तो ज़ख़्म का मरहम नहीं होता,

यकीं है उसपे अच्छी बात है लेकिन ये रखना याद
कि पूरे साल भर में एक सा मौसम नहीं होता,

नशा हो या मोहब्बत हो उतरती चढ़ती रहती है
उतर जाये मोहब्बत फिर तो कोई गम नहीं होता,

पसीना बह गया था काटने में इक पुराना पेड़
मुझे लगता था बूढ़ों में तो इतना दम नहीं होता,

मेरे दुश्मन गिराकर सोचते हैं हार जाऊँगा
मगर ये हौसला मेरा कभी क्यों कम नहीं होता,

मेरा दिल कितना पत्थर है ज़रा देखो इसे आख़िर
ये क्यों इतने ज़ियादा गम में आँखें नम नहीं होता,`,

    aasman: `आसमाँ को कभी नीचे में ठिकाना न मिला,
रहा ऊपर कभी छोटा सा किनारा न मिला,

हम मिले महज़ बिछड़ने के लिये और हुआ
ये कि फिर हमको  बिछड़ने का बहाना न मिला,

मैं यहाँ तन्हा हूँ और इतना ज़ियादा तन्हा
कि मुझे आईने में भी कोई चेहरा न मिला,

घर बनाने के लिए काट दिया मैंने पेड़
और फिर ये कि परिंदे को बसेरा न मिला,

उसके माथे के लिए एक सितारा ढूंढा
पर मुझे ऐसा चमकता हुआ तारा न मिला,

दीपक महापात्रे`,

    bukhar: `बिछड़ जाने से वो ए'तबार रहता नहीं,
तो मैं ये समझूँ कि पहले सा प्यार रहता नहीं,

ख़ुदा अगर कभी कुछ लेता है तो देता भी है
ख़ुदा कभी किसी का कर्ज़दार रहता नहीं,

ख़ुशी से ग़म को भी मैं झेल लेता हूँ यारों
सुना है दर्द कभी यादगार रहता नहीं,

किसी भी काम में आने लगे मज़ा जो कभी
वो काम और कभी रोजगार रहता नहीं,

बुख़ार आते ही माँ याद आती है मुझको
सुना है गोदी में माँ के बुख़ार रहता नहीं,

दीपक महापात्रे`,

    kaho: `कहो कि मेरे रास्ते से हट जाते
या आये और मेरे सीने से लिपट जाये

मैं ऐसा बाँस नहीं बनना चाहता हूँ जो
अना में भूल के तहज़ीब जल्द कट जाये,

ये दरिया है ये समंदर में तो मिलेगा ज़रूर
कभी हुआ कि ये दरिया कहीं भटक जाये,

ख़ुदा से मैं ये दुआ करता हूँ कि उसके लिये
मैं बद्दुआ जो करूँ तो ज़ुबाँ पलट जाये,

मैं उससे मिलते हुये ये कभी भी सोचा नहीं
कि वक़्त जल्दी से जल्दी गुजरते कट जाये,

दीपक महापात्रे`,

    bag: `कभी जो फूलों की रखवाली में भी ध्यान न दे,
यकीं हो ख़ुद पे तभी देना इम्तिहान

यूँ ख़ुद को आजमाने की ख़ातिर तू इम्तिहान न दे,
ज़मीं मेरी है मगर आसमाँ मुहब्बत है

मैं भूल जाऊँ ज़मीं ऐसी तो उड़ान न दे,
गुजार मैं तेरे वादे पे दिन नहीं सकता

सो मुझको तू कभी ऐसी कोई ज़ुबान न दे,
यूँ भूल जाऊँ तुझे तेरे जाने के मैं बाद

सो मुझको तू कभी ऐसे कोई निशान न दे।

– दीपक महापात्रे`
  };

  // हर ग़ज़ल का पहला लाइन निकालकर dropdown में डालना
  const select = document.getElementById('ghazal-select');

  for (const key in ghazals) {
    if (ghazals.hasOwnProperty(key)) {
      // पहली लाइन निकालो
      const firstLine = ghazals[key].split('\n')[0];
      const option = document.createElement('option');
      option.value = key;
      option.textContent = firstLine;
      select.appendChild(option);
    }
  }

  // पढ़ें बटन पर पूरी ग़ज़ल दिखाओ
  function showGhazal() {
    const selectedKey = select.value;
    const textDiv = document.getElementById('ghazal-text');
    if (selectedKey && ghazals[selectedKey]) {
      textDiv.textContent = ghazals[selectedKey];
    } else {
      textDiv.textContent = '';
      alert('कृपया कोई ग़ज़ल चुनें।');
    }
  }
</script>

</body>
</html>
