#pip3.5 install --user sklearn
#pip3.5 install --upgrade --user pandas
#pip3.5 install --upgrade --user IPython

def palace(features):

    import json
    import pickle
    features_py = json.loads(features)
    for key in features_py:
        if type(features_py[key]) is str:
            if len(features_py[key]) == 0:
                features_py[key] = 0
            else:
                features_py[key] = int(float(features_py[key]))
        if type(features_py[key]) is float:
            features_py[key] = int(features_py[key])
    featured_list = [[features_py["MALE"],features_py["IMEs"],features_py["APPLIED"],features_py["ON_TIMELOSS"],features_py["SURGERY"],features_py["Days_Passed_Injury"],features_py["AGE"],features_py["REPORT_DELAY"],features_py["ANKLE"],features_py["ARM"],features_py["ELBOW"],features_py["EYE"],features_py["FACE"],features_py["FOOT"],features_py["FOOT-FEET"],features_py["HAND"],features_py["HEAD"],features_py["HIP"],features_py["INTERNAL_ORGANS"],features_py["KNEE"],features_py["LEG"],features_py["LOW-BACK"],features_py["MID-BACK"],features_py["OTHER_BODY"],features_py["NECK"],features_py["SHOULDER"],features_py["SI"],features_py["TEETH"],features_py["UPPER-BACK"],features_py["WRIST"],features_py["CARPENTER"],features_py["CONSTRUCTION"],features_py["ELECTRICIAN"],features_py["MANUFACTURING"],features_py["MECHANIC"],features_py["MEDICAL"],features_py["OFFICE"],features_py["OTHER_WORK"],features_py["SAFETY"],features_py["RESTAURANT-FASTFOOD"],features_py["RETAIL"],features_py["TRANSPORTATION"],features_py["TRUCKING"],features_py["WAREHOUSE"],features_py["INDUSTRIAL_INJURY"],features_py["OCCUPATIONAL_DISEASE"],features_py["LI"],features_py["OTHER_TYPE"],features_py["PI"],features_py["MENTAL_HEALTH"],features_py["PELVIS"],features_py["HEADACHE"]]]
    pred_model = pickle.load(open("/home/palacelaw/lib/palace_model.pickle", 'rb'))
    guess = pred_model.predict(featured_list)[0]

    probablity = pred_model.predict_proba(featured_list)[0][1]*100

    location = ""
    content = """<html>
<head>
<title>Prediction</title>
    <meta name="viewport" content="width=device-width; initial-scale=1.0; maximum-scale=1.0; user-scalable=0;" />
    <meta name="apple-mobile-web-app-capable" content="no" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    <style>
        body{
            padding:100px 15px 0 15px;
            text-align:center;
            font-size: 46px;
            line-height: 48px;
        }
        .button {
            font-size: 30px;
            line-height: 35px;
            padding:10px;
        }
    </style>
</head>
<body>
    <p>
        Q Score: %s%%
    </p>
    <p>
    <input type="button" value="Again" onCLick="document.location.href = 'http://palacelaw.pythonanywhere.com/bot/'" class="button"/>
    </p>
</body>
</html>"""%(int(round(probablity)))

    return location, content
