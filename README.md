<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>SS Medicine Suggestion & Online Orders</title>
<style>
  :root { --g:#0f9d75; --gd:#0a6f53; --bg:#eefaf5; --card:#fff; --tx:#1d2b27; --mut:#6b7c76; --red:#d64545; --amb:#e49b0f; }
  * { box-sizing:border-box; margin:0; padding:0; font-family:'Segoe UI',Roboto,Arial,sans-serif; }
  body { background:var(--bg); color:var(--tx); min-height:100vh; display:flex; justify-content:center; padding:16px; }
  .app { width:100%; max-width:540px; }
  .page { display:none; background:var(--card); border-radius:18px; padding:24px 20px; box-shadow:0 6px 24px rgba(0,0,0,.08); animation:f .3s; }
  .page.active { display:block; }
  @keyframes f { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:none} }
  h1 { color:var(--gd); font-size:1.7rem; line-height:1.25; }
  h2 { color:var(--gd); margin-bottom:14px; font-size:1.3rem; }
  h3 { margin:14px 0 6px; font-size:1rem; color:var(--gd); }
  .steps { font-size:.8rem; color:var(--mut); margin-bottom:6px; }
  label { display:block; font-weight:600; margin:12px 0 4px; font-size:.9rem; }
  input, select, textarea { width:100%; padding:11px 12px; border:1.5px solid #cfe3db; border-radius:10px; font-size:1rem; background:#fff; }
  input:focus, select:focus, textarea:focus { outline:none; border-color:var(--g); }
  .btns { display:flex; gap:10px; margin-top:20px; }
  button { flex:1; padding:12px; border:none; border-radius:10px; font-size:1rem; font-weight:600; cursor:pointer; }
  .primary { background:var(--g); color:#fff; } .primary:hover { background:var(--gd); }
  .primary:disabled { background:#9bc9bb; cursor:default; }
  .skip { background:#e6efeb; color:var(--tx); }
  .back { background:transparent; color:var(--mut); flex:0 0 auto; padding:12px 8px; }
  .hero { text-align:center; padding:30px 0 6px; }
  .logo { font-size:4rem; }
  .hero p { color:var(--mut); margin:10px 0 24px; }
  .box { border-radius:12px; padding:12px 14px; margin:10px 0; font-size:.92rem; }
  .info { background:#e8f6f0; } .warn { background:#fff3e0; border-left:4px solid var(--amb); }
  .danger { background:#fdeaea; border-left:4px solid var(--red); }
  ul { padding-left:20px; } li { margin:4px 0; }
  .row { display:flex; align-items:center; justify-content:space-between; gap:8px; padding:10px 0; border-bottom:1px dashed #d8e6e0; }
  .row small { color:var(--mut); display:block; }
  .shop { border:1.5px solid #d8e6e0; border-radius:12px; padding:12px; margin:10px 0; cursor:pointer; }
  .shop.sel { border-color:var(--g); background:#f1fbf7; }
  .shop a { color:var(--gd); font-weight:600; text-decoration:none; }
  .qty { width:64px; padding:6px; text-align:center; }
  .inline { display:flex; gap:8px; } .inline button { flex:0 0 auto; padding:0 16px; }
  .custom { background:#f6fbf9; border:1.5px dashed var(--g); border-radius:12px; padding:4px 12px 12px; margin-top:10px; display:none; }
  table { width:100%; border-collapse:collapse; margin:8px 0; font-size:.92rem; }
  td, th { padding:7px 4px; text-align:left; border-bottom:1px solid #e4efe9; } td:last-child, th:last-child { text-align:right; }
  .total td { font-weight:700; font-size:1.05rem; border-top:2px solid var(--g); }
  .stars { font-size:2.2rem; text-align:center; letter-spacing:6px; margin:10px 0; user-select:none; }
  .stars span { cursor:pointer; color:#ccd; } .stars span.on { color:#f5b301; }
  .center { text-align:center; } .err { color:var(--red); font-size:.85rem; margin-top:6px; min-height:1em; }
  .tiny { font-size:.75rem; color:var(--mut); margin-top:12px; text-align:center; }
  .pin { display:inline-block; background:#e8f6f0; color:var(--gd); font-weight:700; border-radius:8px; padding:3px 10px; margin-top:6px; }
</style>
</head>
<body>
<div class="app">

<!-- PAGE 1 : HOME -->
<section class="page active" id="p1">
  <div class="hero">
    <div class="logo">💊</div>
    <h1>SS Medicine Suggestion<br>&amp; Online Orders</h1>
    <p>Men, women &amp; children, hair &amp; skin problems kosam medicine suggestions, food precautions, nearby medical shops &amp; online ordering.</p>
  </div>
  <div class="btns"><button class="primary" onclick="go(2)">Continue →</button></div>
  <p class="tiny">⚠ Idi general information kosam matrame. Doctor advice ki substitute kaadu.</p>
</section>

<!-- PAGE 2 : PATIENT DETAILS -->
<section class="page" id="p2">
  <div class="steps">Step 1 of 5</div>
  <h2>Patient Details</h2>
  <label>Name</label><input id="pname" placeholder="Enter name">
  <label>Age</label><input id="page" type="number" min="0" max="120" placeholder="Enter age" oninput="fillDiseases()">
  <label>Gender</label>
  <select id="pgender" onchange="fillDiseases()"><option value="">-- Select --</option><option>Male</option><option>Female</option><option>Other</option></select>
  <label>Disease / Problem Name</label>
  <select id="pdisease"></select>
  <div class="tiny" style="text-align:left;margin-top:4px">Age &amp; gender batti Women's / Men's / Children's problems kuda kanipistayi.</div>
  <label>Severity (Ratio)</label>
  <select id="pseverity"><option value="">-- Select --</option><option>Low</option><option>Medium</option><option>High</option></select>
  <div class="err" id="err2"></div>
  <div class="btns"><button class="back" onclick="go(1)">← Back</button><button class="primary" onclick="submitDetails()">Continue →</button></div>
</section>

<!-- PAGE 3 : SUGGESTION -->
<section class="page" id="p3">
  <div class="steps">Step 2 of 5</div>
  <h2>Medicine Suggestion</h2>
  <div id="sugg"></div>
  <div class="btns"><button class="back" onclick="go(2)">← Back</button><button class="skip" onclick="go(4)">Skip</button><button class="primary" onclick="go(4)">Continue →</button></div>
</section>

<!-- PAGE 4 : LOCATION, ADDRESS, SHOPS & ORDER ITEMS -->
<section class="page" id="p4">
  <div class="steps">Step 3 of 5</div>
  <h2>Location &amp; Nearby Shops</h2>

  <label>Search by Pincode</label>
  <div class="inline"><input id="pinsearch" type="tel" maxlength="6" placeholder="e.g. 500016"><button class="primary" onclick="pinLookup()">Find</button></div>

  <label>State / UT</label><select id="state" onchange="onState()"></select>
  <label>District</label><select id="district" onchange="onDistrict()"></select>
  <label>Sub-area / Locality</label><select id="area" onchange="onArea()"></select>

  <div class="custom" id="customBox">
    <label>Type your current location / locality</label>
    <input id="customArea" placeholder="e.g. Sai Nagar Colony, Near Bus Stand">
    <label>Pincode</label>
    <input id="customPin" type="tel" maxlength="6" placeholder="6 digit pincode">
    <div class="btns" style="margin-top:10px"><button class="primary" onclick="confirmCustom()">Use this location</button></div>
  </div>

  <div id="pinshow"></div>
  <div class="err" id="errloc"></div>

  <label>Delivery Address (house no, street, landmark)</label>
  <textarea id="daddr" rows="3" placeholder="Full delivery address"></textarea>
  <label>Mobile Number</label>
  <input id="dphone" type="tel" maxlength="10" placeholder="10 digit mobile number">

  <div id="shops"></div>

  <h3>Your Order (<span id="dname"></span>)</h3>
  <div id="items"></div>
  <div class="err" id="err4" style="font-weight:600"></div>
  <div class="btns"><button class="back" onclick="go(3)">← Back</button><button class="skip" onclick="go(6)">Skip</button><button class="primary" onclick="toBill()">Continue →</button></div>
  <p class="tiny">Shop names &amp; phone numbers sample data. Real shop data tho replace cheyandi.</p>
</section>

<!-- PAGE 5 : CONFIRM & BILL -->
<section class="page" id="p5">
  <div class="steps">Step 4 of 5</div>
  <h2>Bill &amp; Delivery Details</h2>
  <div class="box info" id="orderidline"></div>
  <label>Name</label><input id="oname">
  <label>Phone Number</label><input id="ophone" type="tel" maxlength="10" placeholder="10 digit mobile number">
  <label>Delivery Address</label><textarea id="oaddr" rows="3"></textarea>
  <div class="box info" id="locline"></div>
  <h3>🧾 Bill</h3>
  <div id="bill"></div>
  <h3>🛵 Delivery Boy Details</h3>
  <div id="dboy"></div>
  <div class="err" id="err5" style="font-weight:600"></div>
  <div id="ordermsg"></div>
  <div class="btns"><button class="back" onclick="go(4)">← Back</button><button class="primary" id="placeBtn" onclick="placeOrder()">Place Order</button></div>
  <div class="btns"><button class="skip" onclick="go(6)">Skip</button><button class="primary" onclick="continueFromBill()">Continue →</button></div>
</section>

<!-- PAGE 6 : THANK YOU -->
<section class="page" id="p6">
  <div class="center">
    <div class="logo">🙏</div>
    <h2 style="margin-top:8px">Thank you for visiting our site!</h2>
    <p style="color:var(--gd);font-weight:600">SS Medicine Suggestion &amp; Online Orders</p>
  </div>
  <div id="finalsum"></div>
  <h3 class="center">Rate your experience</h3>
  <div class="stars" id="stars"></div>
  <label>Feedback</label>
  <textarea id="fb" rows="3" placeholder="Mee feedback ikkada raayandi..."></textarea>
  <div class="err" id="fbmsg"></div>
  <div class="btns"><button class="primary" onclick="sendFeedback()">Submit</button><button class="skip" onclick="closeApp()">Close</button></div>
</section>

</div>

<script>
/* ================= MEDICAL DATA =================
   Common OTC examples for information only. No doses: follow label / doctor / pharmacist.
   M(child, adult, senior) helper: senior defaults to adult list. */
const M = (child, adult, senior) => ({ child, adult, senior: senior || adult });
const CONSULT = ["Consult a doctor"];

/* ---------- GENERAL ---------- */
const GENERAL = {
  "Fever": { meds:M(["Paracetamol syrup"],["Paracetamol 500 mg tablet"]),
    food:["Drink plenty of water, ORS, coconut water","Eat light food: rice porridge, idli, khichdi","Take rest","Avoid oily, spicy and cold food"],
    doctor:"Fever 3 days kanna ekkuva, 103°F paina unte, or rashes/breathing problem unte doctor ni kalavandi." },
  "Cold & Cough": { meds:M(["Saline nasal drops"],["Cetirizine tablet","Cough lozenges / syrup"],["Cough lozenges / syrup"]),
    food:["Warm water, tulsi/ginger tea","Turmeric milk, pepper rasam","Avoid ice cream, cold drinks","Avoid dust and cold air"],
    doctor:"Cough 1 week kanna ekkuva, chest pain or breathlessness unte doctor ni kalavandi." },
  "Headache": { meds:M(["Paracetamol syrup"],["Paracetamol 500 mg tablet"]),
    food:["Drink enough water","Don't skip meals","Limit tea/coffee","Take proper sleep and avoid screen strain"],
    doctor:"Sudden severe headache, vomiting, vision problem or fits unte immediately hospital ki vellandi." },
  "Body Pain": { meds:M(["Paracetamol syrup"],["Paracetamol 500 mg tablet","Pain relief gel (local)"]),
    food:["Warm water bath, light stretching","Protein foods: dal, eggs, milk","Calcium and Vitamin D rich foods","Avoid heavy oily food"],
    doctor:"Pain 5 days kanna ekkuva, swelling or injury unte doctor ni kalavandi." },
  "Acidity / Gas": { meds:M(CONSULT,["Antacid gel/tablet"]),
    food:["Eat small meals on time","Buttermilk, banana, oats","Avoid spicy, fried, pickles, soda","Don't lie down right after food"],
    doctor:"Chest pain, black stools or continuous vomiting unte doctor ni kalavandi." },
  "Diarrhea / Loose Motions": { meds:M(["ORS solution"],["ORS solution","Probiotic capsule"]),
    food:["ORS, rice kanji, curd rice, banana","Boiled and cooled water only","Avoid street food, milk, spicy food","Wash hands properly"],
    doctor:"Blood in stool, very weak/dry mouth, or 2 days kanna ekkuva unte doctor ni kalavandi. Children and seniors lo jagratta." },
  "Allergy": { meds:M(CONSULT,["Cetirizine tablet","Calamine lotion (skin)"]),
    food:["Avoid the food/dust that triggers allergy","Keep house clean","Drink plenty of water","Avoid seafood/nuts if they trigger it"],
    doctor:"Face/lips swelling or breathing difficulty unte emergency." },
  "Sore Throat": { meds:M(["Warm salt-water gargle (older kids)"],["Throat lozenges"]),
    food:["Warm fluids, soups","Honey with warm water","Avoid cold, fried and sour food","Rest your voice"],
    doctor:"Swallowing kastam or fever tho 3 days kanna ekkuva unte doctor ni kalavandi." }
};

/* ---------- WOMEN ---------- */
const WOMEN = {
  "Menstrual Cramps (Period Pain)": { meds:M(CONSULT,["Paracetamol 500 mg tablet","Hot water bag / heating pad"],CONSULT),
    food:["Warm water, ginger or jeera tea","Iron-rich foods: spinach, dates, jaggery, beetroot","Light walking / gentle yoga","Avoid excess tea, coffee, salty and junk food"],
    doctor:"Pain very severe, daily routine disturb chesthe, or periods tho fainting/vomiting unte gynecologist ni kalavandi." },
  "Irregular Periods": { meds:M(CONSULT,["Consult a gynecologist (hormonal medicines doctor advice tho matrame)"],CONSULT),
    food:["Balanced diet: fruits, vegetables, dal, nuts","Avoid crash diets and skipping meals","Regular sleep and exercise","Manage stress (yoga, walking)"],
    doctor:"3 months kanna ekkuva periods raakapote (pregnancy kaakapothe) gynecologist ni kalavandi." },
  "Heavy Bleeding": { meds:M(CONSULT,["Consult a doctor immediately"]),
    food:["Iron and Vitamin C rich foods: dates, jaggery, amla, leafy vegetables","Drink plenty of fluids","Take rest"],
    doctor:"Pad ni 1-2 gantalaku okasari marchalsi vachte, clots, dizziness, or weakness unte VENTANE doctor/hospital ki vellandi. Self-medication cheyyavaddu." },
  "PCOS / PCOD Symptoms": { meds:M(CONSULT,["Consult a gynecologist (diagnosis + treatment doctor ae chestaru)"],CONSULT),
    food:["High-fibre foods: millets, oats, vegetables","Protein: dal, eggs, paneer","Reduce sugar, maida, fried and packaged foods","Regular exercise 30 min/day, weight control"],
    doctor:"Irregular periods, excess facial hair, acne, weight gain unte tests (ultrasound, hormones) kosam gynecologist ni kalavandi." },
  "Urinary Infection (UTI)": { meds:M(CONSULT,["ORS solution","Consult a doctor for antibiotics (prescription avasaram)"],CONSULT),
    food:["Drink plenty of water (8-10 glasses)","Coconut water, buttermilk","Avoid holding urine","Maintain genital hygiene, wear cotton innerwear"],
    doctor:"Burning urine, fever, back pain or blood in urine unte doctor ni kalavandi. Antibiotics prescription tho matrame." },
  "White Discharge / Vaginal Itching": { meds:M(CONSULT,["Consult a gynecologist (cause batti treatment maaruthundi)"],CONSULT),
    food:["Curd / probiotic foods","Plenty of water","Reduce sugar intake","Keep area clean and dry, avoid harsh soaps"],
    doctor:"Bad smell, colour change, itching ekkuva, or pain unte gynecologist ni kalavandi." },
  "Pregnancy Nausea / Morning Sickness": { meds:M(CONSULT,["Consult your gynecologist before taking ANY medicine"],CONSULT),
    food:["Small, frequent meals","Dry biscuits/toast in the morning","Ginger tea, lemon water, coconut water","Avoid oily, spicy and strong-smelling food"],
    doctor:"Continuous vomiting, water kuda aagakapote, weakness, or weight loss unte vendane doctor ni kalavandi. Pregnancy lo e medicine kuda doctor advice tho matrame." },
  "Anemia / Weakness (Low Iron)": { meds:M(CONSULT,["Iron + folic acid tablet (doctor advice tho)"]),
    food:["Spinach, drumstick leaves, beetroot, pomegranate","Dates, jaggery, ragi, groundnuts","Vitamin C (lemon, amla) tho iron absorb avuthundi","Tea/coffee bhojanam tarvata 1 hour varaku avoid cheyandi"],
    doctor:"Breathlessness, heartbeat ekkuva, pale skin unte Hb test cheyinchukondi." },
  "Breast Pain / Tenderness": { meds:M(CONSULT,["Paracetamol 500 mg tablet","Supportive well-fitting bra"],CONSULT),
    food:["Reduce caffeine and salt","Balanced diet, regular exercise","Warm compress"],
    doctor:"Lump, nipple discharge, skin change or one-sided persistent pain unte vendane doctor ni kalavandi." },
  "Menopause Symptoms (Hot Flashes etc.)": { meds:M(CONSULT,["Calcium + Vitamin D3 tablet (doctor advice tho)"]),
    food:["Calcium-rich foods: milk, curd, ragi, sesame","Vitamin D: morning sunlight","Avoid spicy food, caffeine, alcohol","Regular walking and weight-bearing exercise"],
    doctor:"Heavy bleeding, severe mood changes, or bone pain unte doctor ni kalavandi." }
};

/* ---------- MEN ---------- */
const MEN = {
  "Back Pain / Muscle Strain": { meds:M(CONSULT,["Paracetamol 500 mg tablet","Pain relief gel (local)","Hot water bag / heating pad"]),
    food:["Protein: dal, eggs, milk, paneer","Calcium and Vitamin D rich foods","Plenty of water","Avoid heavy lifting; keep correct posture"],
    doctor:"Pain legs ki spread aithe, numbness, or urine/motion control problem unte vendane doctor ni kalavandi." },
  "Joint Pain / Stiffness": { meds:M(CONSULT,["Paracetamol 500 mg tablet","Pain relief gel (local)"]),
    food:["Calcium: milk, ragi, sesame","Omega-3: fish, walnuts, flaxseed","Maintain healthy weight","Avoid too much salt and fried food"],
    doctor:"Joints lo swelling, redness, or morning stiffness 1 hour kanna ekkuva unte doctor ni kalavandi." },
  "Fatigue / Low Energy": { meds:M(CONSULT,["Multivitamin tablet"]),
    food:["Balanced meals: dal, vegetables, fruits, eggs","Nuts, banana, dates for energy","Plenty of water; limit alcohol and smoking","7-8 hours sleep, daily exercise"],
    doctor:"Weakness 2 weeks kanna ekkuva unte blood sugar, thyroid, Hb tests cheyinchukondi." },
  "Urinary Problems (Frequent / Burning)": { meds:M(CONSULT,["ORS solution","Consult a doctor (infection/prostate cause ayite prescription avasaram)"],CONSULT),
    food:["Plenty of water","Coconut water, buttermilk","Reduce tea, coffee, alcohol","Don't hold urine"],
    doctor:"Burning, blood in urine, weak flow, or night lo tarachuga urine ki velthe urologist ni kalavandi (50+ years lo mukhyam)." },
  "Sexual Health Concerns": { meds:M(CONSULT,["Consult a doctor / urologist (self-medication vaddu)"],CONSULT),
    food:["Balanced diet, regular exercise","Reduce alcohol, quit smoking","Manage stress, proper sleep","Diabetes/BP check cheyinchukondi"],
    doctor:"Ivi diabetes, BP, stress valla kuda raavachu. Private ga doctor/urologist ni kalavandi. Online lo dorike 'power tablets' teesukovaddu." },
  "Sleep Problems / Snoring": { meds:M(CONSULT,["Consult a doctor (sleeping pills self-medication vaddu)"],CONSULT),
    food:["Light dinner 2-3 hours before sleep","Avoid tea/coffee/alcohol in evening","Fixed sleep time, no mobile in bed","Weight control, side-sleeping"],
    doctor:"Loud snoring tho breath aagadam, pagati poota nidra, or morning headaches unte sleep specialist ni kalavandi." }
};

/* ---------- CHILDREN (shown for age 14 and below). Medicines same for every age group. ---------- */
const kid = (meds, food, doctor) => ({ meds:M(meds,meds,meds), food, doctor });
const CHILD = {
  "Diaper Rash (Babies)": kid(["Zinc oxide cream"],
    ["Change diaper often","Clean with water/soft wipes, pat dry","Let skin air-dry without diaper for some time","Avoid scented wipes and powders"],
    "Rash 3 days kanna ekkuva, blisters, or fever tho unte pediatrician ni kalavandi."),
  "Teething Pain": kid(["Consult a doctor"],
    ["Clean teething ring (chilled, not frozen)","Gently massage gums with clean finger","Give soft, cool foods if baby eats solids","Avoid honey for babies below 1 year"],
    "High fever, diarrhea or very long crying unte teething kaadu, doctor ni kalavandi."),
  "Constipation (Children)": kid(["Consult a doctor"],
    ["More water and fibre: fruits (papaya, banana), vegetables","Whole grains, ragi, oats","Regular toilet routine","Reduce maida, biscuits, junk food"],
    "Stomach pain, blood in stool, or 1 week kanna ekkuva constipation unte doctor ni kalavandi."),
  "Intestinal Worms": kid(["Consult a doctor (deworming tablet doctor advice tho)"],
    ["Wash hands before eating and after toilet","Cut nails short; wear footwear","Wash fruits and vegetables; drink clean water","Keep home and toilets clean"],
    "Stomach pain, weight loss, anal itching unte doctor ni kalavandi."),
  "Loss of Appetite (Children)": kid(["Consult a doctor"],
    ["Small, frequent, colourful meals","Eggs, dal, ragi malt, banana, nuts (age ki taggattu)","Avoid biscuits/chips/juice before meals","Don't force-feed; fix meal times"],
    "Weight not increasing, tiredness, or pale look unte pediatrician ni kalavandi."),
  "Vomiting & Dehydration (Children)": kid(["ORS solution"],
    ["ORS small sips tarachuga","Rice kanji, banana, curd rice when vomiting aagaka","Boiled & cooled water","Avoid oily, spicy and outside food"],
    "Urine ekkuvasepu raakapote, very sleepy, sunken eyes, or continuous vomiting unte VENTANE hospital ki vellandi."),
  "Ear Pain (Children)": kid(["Paracetamol syrup"],
    ["Keep ear dry; don't put oil/drops without doctor advice","Don't use ear buds","Warm cloth outside ear (gently)"],
    "Ear nundi discharge, fever, or pain ekkuva unte doctor ni kalavandi."),
  "Bedwetting": kid(["Consult a doctor"],
    ["Less fluids 2 hours before bed","Toilet before sleeping","Praise dry nights; don't scold","Avoid tea/cola/chocolate evening"],
    "5-6 years paina continuous ga ayite or sudden ga start aithe pediatrician ni kalavandi.")
};

/* ---------- HAIR ---------- */
const HAIR = {
  "Hair Fall": { meds:M(CONSULT,["Biotin tablet (doctor advice tho)","Hair oil (coconut/castor)"]),
    food:["Protein: dal, eggs, paneer, sprouts","Iron: spinach, dates, beetroot","Vitamin C: amla, lemon, orange","Reduce stress, sleep well; avoid harsh chemicals/heat"],
    doctor:"Sudden heavy hair fall, round bald patches, or thyroid/PCOS symptoms unte dermatologist ni kalavandi." },
  "Dandruff": { meds:M(CONSULT,["Anti-dandruff shampoo"]),
    food:["Zinc & omega-3: nuts, seeds, fish","Reduce sugar and oily food","Plenty of water","Wash hair regularly; don't share combs/towels"],
    doctor:"Red, painful or thick scaly scalp unte dermatologist ni kalavandi." },
  "Dry & Frizzy Hair / Split Ends": { meds:M(CONSULT,["Hair oil (coconut/castor)"]),
    food:["Protein, omega-3, plenty of water","Avoid frequent hot-water wash and heat styling","Trim hair every 2-3 months"],
    doctor:"Hair break ayyi chala thin ayite thyroid/nutrition tests cheyinchukondi." },
  "Scalp Itching / Head Lice": { meds:M(CONSULT,["Anti-lice lotion","Anti-dandruff shampoo"],["Anti-lice lotion","Anti-dandruff shampoo"]),
    food:["Keep scalp clean and dry","Wash combs, bedsheets, caps in hot water","Don't share combs/pillows","Check all family members"],
    doctor:"Sores, pus, or itching 1 week kanna ekkuva unte doctor ni kalavandi. Children ki lice products doctor advice tho." },
  "Premature Greying": { meds:M(CONSULT,["Consult a doctor (Vitamin B12 / thyroid tests)"]),
    food:["Vitamin B12: milk, curd, eggs","Iron & copper: nuts, seeds, dates","Quit smoking; manage stress","Balanced diet with fruits and vegetables"],
    doctor:"Chinna vayasu lo ekkuva greying unte B12, thyroid tests kosam doctor ni kalavandi." }
};

/* ---------- SKIN ---------- */
const SKIN = {
  "Acne / Pimples": { meds:M(CONSULT,["Benzoyl peroxide gel","Sunscreen SPF 30+"]),
    food:["Plenty of water","Fruits, vegetables, nuts","Reduce sugar, fried and dairy-heavy foods if they trigger it","Wash face twice daily; don't pop pimples"],
    doctor:"Deep painful cysts, scarring, or acne 2 months try chesina taggakapote dermatologist ni kalavandi." },
  "Fungal Infection (Ringworm / Itching)": { meds:M(CONSULT,["Clotrimazole cream"]),
    food:["Reduce sugar and refined carbs","Wear loose cotton clothes","Keep skin dry; dry well after bath","Don't share towels/clothes; wash clothes in hot water"],
    doctor:"2-4 weeks lo taggakapote or spread aithe dermatologist ni kalavandi. Children/diabetes unte doctor advice tho." },
  "Scabies (Severe Night Itching)": { meds:M(CONSULT,["Permethrin cream (doctor advice tho)"]),
    food:["Balanced diet, plenty of water","Wash bedsheets/clothes in hot water, sun-dry","Whole family treatment avasaram avvachu","Don't scratch; keep nails short"],
    doctor:"Scabies ante contagious, doctor diagnose chesi treatment ivvali. Infants/pregnant ki doctor advice must." },
  "Eczema / Dry Skin": { meds:M(CONSULT,["Moisturizing lotion"]),
    food:["Plenty of water","Omega-3: nuts, seeds, fish","Avoid known allergens","Short lukewarm baths; avoid harsh soaps; moisturize daily"],
    doctor:"Cracked, bleeding, oozing skin or sleep disturb chese itching unte dermatologist ni kalavandi." },
  "Heat Rash / Prickly Heat": { meds:M(["Calamine lotion (skin)"],["Calamine lotion (skin)"]),
    food:["Plenty of water, coconut water, buttermilk","Light, loose cotton clothes","Cool bath, stay in shade/ventilation","Avoid oily creams on rash"],
    doctor:"Rash with fever, pus, or 1 week kanna ekkuva unte doctor ni kalavandi." },
  "Insect Bite / Sting": { meds:M(["Calamine lotion (skin)"],["Calamine lotion (skin)","Cetirizine tablet"]),
    food:["Plenty of water","Cold compress on bite","Don't scratch","Use mosquito nets/repellent"],
    doctor:"Face/lips swelling, breathing difficulty, or spreading redness unte emergency." },
  "Minor Cut / Burn": { meds:M(["Antiseptic solution/cream"],["Antiseptic solution/cream","Aloe vera gel"]),
    food:["Protein and Vitamin C for healing","Plenty of water","Burn ki: cool running water 10-15 min (no ice, no toothpaste/butter)","Keep wound clean and covered"],
    doctor:"Deep cut, bleeding aagakapote, big blisters, face/hand burn, or infection signs (pus, swelling) unte hospital ki vellandi." },
  "Sunburn / Tanning": { meds:M(CONSULT,["Aloe vera gel","Sunscreen SPF 30+"]),
    food:["Plenty of water, coconut water","Fruits rich in Vitamin C","Stay out of sun 10am-4pm; use hat/umbrella","Apply sunscreen daily"],
    doctor:"Blisters, fever, or severe pain unte doctor ni kalavandi." }
};

const CATEGORIES = [
  { label:"General Health",         data:GENERAL, show:() => true },
  { label:"Women's Health 👩",       data:WOMEN,   show:() => $('pgender').value==="Female" },
  { label:"Men's Health 👨",         data:MEN,     show:() => $('pgender').value==="Male" },
  { label:"Children's Health 👶",    data:CHILD,   show:() => { const a=parseInt($('page').value); return !isNaN(a) && a<=14; } },
  { label:"Hair Problems 💇",        data:HAIR,    show:() => true },
  { label:"Skin Diseases 🧴",        data:SKIN,    show:() => true }
];

const PRICES = {
  "Paracetamol syrup":55,"Paracetamol 500 mg tablet":30,"Saline nasal drops":65,"Cetirizine tablet":25,"Cough lozenges / syrup":90,
  "Pain relief gel (local)":110,"Antacid gel/tablet":70,"ORS solution":25,"Probiotic capsule":95,"Calamine lotion (skin)":80,"Throat lozenges":45,
  "Hot water bag / heating pad":180,"Iron + folic acid tablet (doctor advice tho)":60,"Calcium + Vitamin D3 tablet (doctor advice tho)":120,
  "Multivitamin tablet":140,"Zinc oxide cream":90,"Anti-dandruff shampoo":220,"Anti-lice lotion":130,"Biotin tablet (doctor advice tho)":150,
  "Hair oil (coconut/castor)":120,"Benzoyl peroxide gel":120,"Clotrimazole cream":75,"Permethrin cream (doctor advice tho)":110,
  "Moisturizing lotion":180,"Antiseptic solution/cream":60,"Aloe vera gel":100,"Sunscreen SPF 30+":350
};
const orderable = n => PRICES[n] > 0;
const DELIVERY = 30;

/* ================= LOCATION DATA =================
   State -> District -> "Area:Pincode,Area:Pincode"
   Telangana & Andhra Pradesh detailed; other states: major districts/cities.
   For any other place use "Search by Pincode" or choose "Type my location". Verify pincodes with India Post. */
const GEO = {
"Telangana": {
 "Hyderabad":"Ameerpet:500016,Begumpet:500016,Kukatpally:500072,KPHB Colony:500072,Madhapur:500081,Gachibowli:500032,Kondapur:500084,Miyapur:500049,Banjara Hills:500034,Jubilee Hills:500033,Secunderabad:500003,Dilsukhnagar:500060,LB Nagar:500074,Uppal:500039,Charminar:500002,Mehdipatnam:500028,Tarnaka:500017,Abids:500001,Nampally:500001,Manikonda:500089,Attapur:500048",
 "Medchal-Malkajgiri":"Medchal:501401,Malkajgiri:500047,Kompally:500014,Alwal:500010,Bowenpally:500011",
 "Rangareddy":"Shamshabad:501218,Ibrahimpatnam:501506,Chevella:501503,Shadnagar:509216,Rajendranagar:500030,Hayathnagar:501505",
 "Sangareddy":"Sangareddy:502001,Patancheru:502319,Zaheerabad:502220,Ramachandrapuram:502032",
 "Vikarabad":"Vikarabad:501101","Medak":"Medak:502110","Siddipet":"Siddipet:502103","Kamareddy":"Kamareddy:503111",
 "Nizamabad":"Nizamabad:503001,Bodhan:503185,Armoor:503224",
 "Karimnagar":"Karimnagar:505001,Huzurabad:505468,Jammikunta:505122",
 "Peddapalli":"Peddapalli:505172,Godavarikhani:505209","Rajanna Sircilla":"Sircilla:505301","Jagtial":"Jagtial:505327",
 "Warangal":"Warangal:506002,Narsampet:506132,Parkal:506164","Hanumakonda":"Hanamkonda:506001,Kazipet:506003",
 "Jangaon":"Jangaon:506167","Mahabubabad":"Mahabubabad:506101","Jayashankar Bhupalpally":"Bhupalpally:506169","Mulugu":"Mulugu:506343",
 "Khammam":"Khammam:507001,Madhira:507203,Sathupalli:507303,Wyra:507165","Bhadradri Kothagudem":"Kothagudem:507101,Bhadrachalam:507111",
 "Nalgonda":"Nalgonda:508001,Miryalaguda:508207,Devarakonda:508248,Nakrekal:508218","Suryapet":"Suryapet:508213","Yadadri Bhuvanagiri":"Bhongir:508116",
 "Mahabubnagar":"Mahabubnagar:509001,Jadcherla:509301,Devarkadra:509204","Nagarkurnool":"Nagarkurnool:509209","Wanaparthy":"Wanaparthy:509103",
 "Jogulamba Gadwal":"Gadwal:509125","Narayanpet":"Narayanpet:509210",
 "Adilabad":"Adilabad:504001","Nirmal":"Nirmal:504106","Mancherial":"Mancherial:504208","Kumuram Bheem Asifabad":"Asifabad:504293"
},
"Andhra Pradesh": {
 "Visakhapatnam":"Visakhapatnam GPO:530001,MVP Colony:530017,Dwaraka Nagar:530016,Seethammadhara:530013,Gajuwaka:530026,Madhurawada:530048",
 "Anakapalli":"Anakapalli:531001","Alluri Sitharama Raju":"Paderu:531024","Vizianagaram":"Vizianagaram:535001","Parvathipuram Manyam":"Parvathipuram:535501",
 "Srikakulam":"Srikakulam:532001","Kakinada":"Kakinada:533001","East Godavari":"Rajahmundry:533101","Konaseema":"Amalapuram:533201",
 "West Godavari":"Bhimavaram:534201","Eluru":"Eluru:534001",
 "NTR":"Vijayawada:520001,Benz Circle:520010,Governorpet:520002,Patamata:520010,Gunadala:520004,Auto Nagar:520007",
 "Krishna":"Machilipatnam:521001","Guntur":"Guntur:522001,Brodipet:522002,Tenali:522201,Mangalagiri:522503","Palnadu":"Narasaraopet:522601",
 "Bapatla":"Bapatla:523101","Prakasam":"Ongole:523001","Nellore":"Nellore:524001","Tirupati":"Tirupati:517501,Renigunta:517520,Chandragiri:517101",
 "Chittoor":"Chittoor:517001","Annamayya":"Rayachoti:516269","YSR Kadapa":"Kadapa:516001","Anantapur":"Anantapur:515001",
 "Sri Sathya Sai":"Puttaparthi:515134","Kurnool":"Kurnool:518001","Nandyal":"Nandyal:518501"
},
"Karnataka": { "Bengaluru Urban":"Koramangala:560034,Indiranagar:560038,Whitefield:560066,Jayanagar:560011,MG Road:560001","Mysuru":"Mysuru:570001","Dakshina Kannada":"Mangaluru:575001","Dharwad":"Hubballi-Dharwad:580001","Belagavi":"Belagavi:590001" },
"Tamil Nadu": { "Chennai":"T Nagar:600017,Adyar:600020,Anna Nagar:600040,Egmore:600008","Coimbatore":"Coimbatore:641001","Madurai":"Madurai:625001","Tiruchirappalli":"Tiruchirappalli:620001","Salem":"Salem:636001" },
"Kerala": { "Thiruvananthapuram":"Thiruvananthapuram:695001","Ernakulam":"Kochi:682001","Kozhikode":"Kozhikode:673001","Thrissur":"Thrissur:680001" },
"Maharashtra": { "Mumbai City":"Fort:400001,Colaba:400005","Mumbai Suburban":"Bandra:400050,Andheri:400053","Pune":"Pune City:411001,Kothrud:411038","Nagpur":"Nagpur:440001","Nashik":"Nashik:422001" },
"Delhi": { "Central Delhi":"Connaught Place:110001,Karol Bagh:110005","South West Delhi":"Dwarka:110075","New Delhi":"New Delhi:110002" },
"Gujarat": { "Ahmedabad":"Ahmedabad:380001","Surat":"Surat:395001","Vadodara":"Vadodara:390001","Rajkot":"Rajkot:360001" },
"Rajasthan": { "Jaipur":"Jaipur:302001","Jodhpur":"Jodhpur:342001","Udaipur":"Udaipur:313001" },
"Uttar Pradesh": { "Lucknow":"Lucknow:226001","Kanpur Nagar":"Kanpur:208001","Varanasi":"Varanasi:221001","Agra":"Agra:282001","Prayagraj":"Prayagraj:211001" },
"West Bengal": { "Kolkata":"Park Street:700016,Salt Lake:700091,Esplanade:700069","Howrah":"Howrah:711101","Darjeeling":"Darjeeling:734101" },
"Bihar": { "Patna":"Patna:800001","Gaya":"Gaya:823001" },
"Madhya Pradesh": { "Bhopal":"Bhopal:462001","Indore":"Indore:452001","Gwalior":"Gwalior:474001" },
"Odisha": { "Khordha":"Bhubaneswar:751001","Cuttack":"Cuttack:753001" },
"Assam": { "Kamrup Metropolitan":"Guwahati:781001" },
"Punjab": { "Ludhiana":"Ludhiana:141001","Amritsar":"Amritsar:143001" },
"Haryana": { "Gurugram":"Gurugram:122001","Faridabad":"Faridabad:121001" },
"Jharkhand": { "Ranchi":"Ranchi:834001" },
"Chhattisgarh": { "Raipur":"Raipur:492001" },
"Uttarakhand": { "Dehradun":"Dehradun:248001" },
"Himachal Pradesh": { "Shimla":"Shimla:171001" },
"Goa": { "North Goa":"Panaji:403001" },
"Jammu and Kashmir": { "Srinagar":"Srinagar:190001","Jammu":"Jammu:180001" },
"Ladakh": { "Leh":"Leh:194101" },
"Chandigarh": { "Chandigarh":"Sector 17:160017" },
"Puducherry": { "Puducherry":"Puducherry:605001" },
"Arunachal Pradesh": { "Papum Pare":"Itanagar:791111" },
"Manipur": { "Imphal West":"Imphal:795001" },
"Meghalaya": { "East Khasi Hills":"Shillong:793001" },
"Mizoram": { "Aizawl":"Aizawl:796001" },
"Nagaland": { "Kohima":"Kohima:797001" },
"Sikkim": { "Gangtok":"Gangtok:737101" },
"Tripura": { "West Tripura":"Agartala:799001" },
"Andaman and Nicobar Islands": { "South Andaman":"Port Blair:744101" },
"Lakshadweep": { "Lakshadweep":"Kavaratti:682555" },
"Dadra and Nagar Haveli and Daman and Diu": { "Daman":"Daman:396210" }
};
const CUSTOM = "__custom__";

/* ================= STATE ================= */
const S = { name:"", age:0, gender:"", disease:"", severity:"", loc:null, shop:null, order:[], address:"", rating:0, orderId:null };
const $ = id => document.getElementById(id);
const parseAreas = str => str.split(',').map(x=>{ const i=x.lastIndexOf(':'); return {name:x.slice(0,i), pin:x.slice(i+1)}; });
const ageGroup = a => a<12 ? "child" : a>=60 ? "senior" : "adult";
const allDiseases = () => Object.assign({}, ...CATEGORIES.map(c=>c.data));
const isIn = (cat, d) => !!cat[d];

function go(n){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  $('p'+n).classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
  if(n===3) renderSuggestion();
  if(n===4) renderOrderPage();
  if(n===5) renderBill();
  if(n===6) renderFinal();
}

/* ================= PAGE 2 ================= */
function fillDiseases(){
  const keep = $('pdisease').value;
  let h = '<option value="">-- Select disease / problem --</option>';
  CATEGORIES.forEach(c=>{
    if(c.show()) h += `<optgroup label="${c.label}">` + Object.keys(c.data).map(d=>`<option>${d}</option>`).join('') + '</optgroup>';
  });
  $('pdisease').innerHTML = h;
  if([...$('pdisease').options].some(o=>o.value===keep && keep)) $('pdisease').value = keep;
}
fillDiseases();

function submitDetails(){
  const name=$('pname').value.trim(), age=parseInt($('page').value), g=$('pgender').value, d=$('pdisease').value, s=$('pseverity').value;
  if(!name) return $('err2').textContent="Please enter name";
  if(isNaN(age)||age<0||age>120) return $('err2').textContent="Please enter a valid age (0-120)";
  if(!g) return $('err2').textContent="Please select gender";
  if(!d) return $('err2').textContent="Please select disease / problem";
  if(!s) return $('err2').textContent="Please select severity";
  $('err2').textContent="";
  Object.assign(S,{name,age,gender:g,disease:d,severity:s});
  go(3);
}

/* ================= PAGE 3 ================= */
function renderSuggestion(){
  const D = allDiseases()[S.disease], grp = ageGroup(S.age);
  const label = {child:"Child (below 12)", adult:"Adult (12-59)", senior:"Senior (60+)"}[grp];
  let h = `<div class="box info"><b>${S.name}</b> · ${S.age} yrs · ${S.gender} · ${S.disease} · Severity: <b>${S.severity}</b><br>Age group: ${label}</div>`;
  if(S.severity==="High") h += `<div class="box danger">🚨 Severity <b>High</b> — self-medication kakunda, <b>dayachesi doctor ni immediately kalavandi</b>.</div>`;
  h += `<h3>💊 Suggested Medicines / Care</h3><ul>${D.meds[grp].map(m=>`<li>${m}</li>`).join('')}</ul>`;
  h += `<div class="box warn">Dose: medicine label lo unnattu or doctor/pharmacist cheppinattu matrame teesukondi. Allergy unte teesukovaddu.</div>`;
  if(S.gender==="Female" && !isIn(WOMEN,S.disease)) h += `<div class="box warn">👩 Pregnant / breastfeeding aithe, e medicine teesukune mundu doctor ni adagandi.</div>`;
  if(isIn(WOMEN,S.disease)) h += `<div class="box warn">👩 Women's health problems lo correct cause telusukovadaniki gynecologist consultation chala mukhyam.</div>`;
  if(isIn(MEN,S.disease)) h += `<div class="box warn">👨 Persistent ga unte specialist (physician/urologist) ni kalavandi.</div>`;
  if(isIn(CHILD,S.disease) || grp==="child") h += `<div class="box warn">👶 Pillalaku doctor (pediatrician) advice tho matrame medicine/cream ivvandi. Babies lo self-medication vaddu.</div>`;
  if(isIn(SKIN,S.disease)) h += `<div class="box warn">🧴 Kotha cream/lotion mundu chinna patch test cheyandi. Steroid creams doctor advice lekunda vaadakandi.</div>`;
  if(isIn(HAIR,S.disease)) h += `<div class="box warn">💇 Hair results ki 2-3 months paduthundi. Daily use mundu patch test cheyandi.</div>`;
  if(grp==="senior") h += `<div class="box warn">👴 BP, sugar, heart problems unte doctor advice tho matrame teesukondi.</div>`;
  h += `<h3>🥗 Food / Home Care Precautions</h3><ul>${D.food.map(f=>`<li>${f}</li>`).join('')}</ul>`;
  h += `<div class="box danger">🩺 ${D.doctor}</div>`;
  $('sugg').innerHTML = h;
}

/* ================= PAGE 4 : LOCATION ================= */
function initStates(){
  $('state').innerHTML = '<option value="">-- Select State / UT --</option>' + Object.keys(GEO).sort().map(s=>`<option>${s}</option>`).join('');
  $('district').innerHTML = '<option value="">-- Select District --</option>';
  $('area').innerHTML = '<option value="">-- Select Area --</option>';
}
function onState(){
  const s = $('state').value;
  $('district').innerHTML = '<option value="">-- Select District --</option>' + (s ? Object.keys(GEO[s]).sort().map(d=>`<option>${d}</option>`).join('') : '');
  $('area').innerHTML = '<option value="">-- Select Area --</option>';
  $('customBox').style.display='none'; clearLoc();
}
function onDistrict(){
  const s=$('state').value, d=$('district').value;
  $('area').innerHTML = '<option value="">-- Select Area --</option>' +
    (d ? parseAreas(GEO[s][d]).map(a=>`<option value="${a.name}">${a.name} (${a.pin})</option>`).join('') : '') +
    `<option value="${CUSTOM}">✏️ Type my current location (not in list)</option>`;
  $('customBox').style.display='none'; clearLoc();
}
function onArea(){
  const s=$('state').value, d=$('district').value, a=$('area').value;
  if(a===CUSTOM){ clearLoc(); $('customBox').style.display='block'; $('customArea').focus(); return; }
  $('customBox').style.display='none';
  if(!a) return clearLoc();
  const found = parseAreas(GEO[s][d]).find(x=>x.name===a);
  setLoc({state:s,district:d,area:a,pin:found.pin});
}
function confirmCustom(){
  const area = $('customArea').value.trim(), pin = $('customPin').value.trim();
  if(area.length<3) return $('errloc').textContent="Please type your location / locality name";
  if(!/^[1-9]\d{5}$/.test(pin)) return $('errloc').textContent="Enter a valid 6 digit pincode";
  setLoc({state:$('state').value, district:$('district').value, area, pin, custom:true});
}
function clearLoc(){ S.loc=null; S.shop=null; $('pinshow').innerHTML=''; $('shops').innerHTML=''; }
function setLoc(loc){
  S.loc = loc; S.shop = null;
  $('errloc').textContent="";
  $('pinshow').innerHTML = `<span class="pin">📮 ${loc.area} · Pincode: ${loc.pin}</span>`;
  renderShops();
}
function pinLookup(){
  const pin = $('pinsearch').value.trim();
  if(!/^[1-9]\d{5}$/.test(pin)) return $('errloc').textContent="Enter a valid 6 digit pincode";
  for(const s in GEO) for(const d in GEO[s]) for(const a of parseAreas(GEO[s][d])){
    if(a.pin===pin){
      initStates();
      $('state').value = s; onState();
      $('state').value = s; $('district').value = d; onDistrict();
      $('district').value = d; $('area').value = a.name;
      return setLoc({state:s,district:d,area:a.name,pin});
    }
  }
  // Not in built-in list: ask user to type the locality
  initStates();
  $('customBox').style.display='block'; $('customPin').value = pin; $('customArea').focus();
  clearLoc();
  $('errloc').textContent="Ee pincode list lo ledu. Mee locality name type chesi 'Use this location' press cheyandi.";
}

/* Sample shops generated per area. Replace with your real shop database / API. */
function shopsFor(loc){
  const names = ["Sri Sai Medicals","Apollo Pharmacy","MedPlus"];
  return names.map((n,i)=>({ n:`${n} - ${loc.area}`, p:`9${loc.pin}0${i}0` }));
}
function renderShops(){
  if(!S.loc){ $('shops').innerHTML=''; return; }
  const list = shopsFor(S.loc);
  $('shops').innerHTML = `<h3>🏪 Shops near ${S.loc.area} (${S.loc.pin})</h3>` + list.map((s,i)=>`
    <div class="shop ${S.shop&&S.shop.n===s.n?'sel':''}" onclick="pickShop(${i})">
      <b>${s.n}</b><br>📍 ${S.loc.area}${S.loc.district?', '+S.loc.district:''} - ${S.loc.pin}<br>
      📞 <a href="tel:${s.p}" onclick="event.stopPropagation()">${s.p}</a>
    </div>`).join('');
}
function pickShop(i){ S.shop = shopsFor(S.loc)[i]; renderShops(); }

/* ================= PAGE 4 : ORDER ITEMS ================= */
function renderOrderPage(){
  $('dname').textContent = S.disease;
  if(!$('state').options.length) initStates();
  const meds = allDiseases()[S.disease].meds[ageGroup(S.age)].filter(orderable);
  const chosen = new Set(S.order.map(o=>o.name));
  $('items').innerHTML = meds.length ? meds.map(m=>`
    <div class="row">
      <label style="margin:0;font-weight:500;display:flex;gap:8px;align-items:center">
        <input type="checkbox" style="width:auto" data-name="${m}" ${chosen.has(m)?'checked':''}>
        <span>${m}<small>₹${PRICES[m]} each</small></span>
      </label>
      <input class="qty" type="number" min="1" max="10" value="${(S.order.find(o=>o.name===m)||{}).qty||1}" data-q="${m}">
    </div>`).join('') : '<div class="box warn">Ee problem ki online order cheyadaniki OTC items levu. Doctor ni kalavandi (Skip press cheyyandi).</div>';
}
/* Show an error right next to the Continue button and bring it into view */
function fail(id, msg){
  const el = $(id); el.textContent = "⚠ " + msg;
  el.scrollIntoView({behavior:'smooth', block:'center'});
  return false;
}
function toBill(){
  // If the person typed a custom location but forgot to press "Use this location", confirm it automatically
  if(!S.loc && $('customBox').style.display==='block'){
    const area = $('customArea').value.trim(), pin = $('customPin').value.trim();
    if(area.length>=3 && /^[1-9]\d{5}$/.test(pin)) setLoc({state:$('state').value, district:$('district').value, area, pin, custom:true});
  }
  const addr = $('daddr').value.trim(), phone = $('dphone').value.trim();
  const checks=[...document.querySelectorAll('#items input[type=checkbox]:checked')];
  const orderableCount = document.querySelectorAll('#items input[type=checkbox]').length;

  if(!S.loc)               return fail('err4',"Please select your area, type your location, or search by pincode");
  if(addr.length<8)        return fail('err4',"Please enter your full delivery address (house no, street, landmark)");
  if(!/^[6-9]\d{9}$/.test(phone)) return fail('err4',"Please enter a valid 10 digit mobile number");
  if(!S.shop)              return fail('err4',"Please tap one medical shop from the list above");
  if(orderableCount && !checks.length) return fail('err4',"Please tick at least one medicine to order");

  S.address = addr; S.phone = phone;
  S.order = checks.map(c=>{ const n=c.dataset.name; const q=Math.max(1,parseInt(document.querySelector(`[data-q="${n}"]`).value)||1); return {name:n,qty:q,price:PRICES[n]}; });
  S.orderId = null; S.delivery = null; S.preview = null;   // fresh bill each time
  $('err4').textContent=""; go(5);
}

/* ================= PAGE 5 ================= */
/* Sample delivery boy, generated from the pincode. Replace with real rider assignment from your backend. */
function makeDelivery(){
  const riders = ["Ravi Kumar","Suresh Reddy","Anil Naidu","Venkatesh","Mahesh Babu","Srinivas Rao"];
  const seed = parseInt(S.loc.pin,10) + S.order.length;
  const code = ["TS09","TS08","AP39","AP16","KA01","TN09"][seed % 6];
  return {
    name: riders[seed % riders.length],
    phone: "9" + String(seed * 7919).padStart(9,"0").slice(-9),
    vehicle: `${code} ${String.fromCharCode(65+seed%26)}${String.fromCharCode(65+(seed*3)%26)} ${1000 + (seed*37)%9000}`,
    eta: `${25 + seed%20}-${45 + seed%15} minutes`
  };
}
function renderBill(){
  $('oname').value  = $('oname').value  || S.name;
  $('ophone').value = $('ophone').value || S.phone || "";
  $('oaddr').value  = $('oaddr').value  || S.address || "";
  $('locline').innerHTML = S.loc ? `📍 Delivery area: <b>${S.loc.area}${S.loc.district?', '+S.loc.district:''}${S.loc.state?', '+S.loc.state:''} - ${S.loc.pin}</b>` : 'Area not selected';

  if(!S.order.length){
    $('orderidline').innerHTML = 'No online order for this problem.';
    $('bill').innerHTML = '<div class="box warn">Ee problem ki online order cheyadaniki OTC items levu, doctor ni kalavandi. Continue nokkandi.</div>';
    $('dboy').innerHTML = '<div class="box info">Order lekapoyaka delivery boy assign avvadu.</div>';
    $('placeBtn').style.display = 'none';
    return;
  }
  $('placeBtn').style.display = '';
  if(!S.orderId){
    $('placeBtn').disabled = false; $('placeBtn').textContent = "Place Order"; $('ordermsg').innerHTML = "";
  }
  S.preview = S.preview || ("SS" + Date.now().toString().slice(-7));
  S.delivery = S.delivery || makeDelivery();
  const id = S.orderId || S.preview;
  $('orderidline').innerHTML = `🧾 Order ID: <b>${id}</b> · Status: <b>${S.orderId ? 'Confirmed ✅' : 'Not placed yet'}</b>`;

  const sub = S.order.reduce((t,o)=>t+o.qty*o.price,0), total = sub+DELIVERY;
  $('bill').innerHTML = `
    <div class="box info">Shop: <b>${S.shop.n}</b> · 📞 ${S.shop.p}</div>
    <table><tr><th>Item</th><th>Qty × ₹</th><th>Amount</th></tr>
    ${S.order.map(o=>`<tr><td>${o.name}</td><td>${o.qty} × ${o.price}</td><td>₹${o.qty*o.price}</td></tr>`).join('')}
    <tr><td colspan="2">Subtotal</td><td>₹${sub}</td></tr>
    <tr><td colspan="2">Delivery charge</td><td>₹${DELIVERY}</td></tr>
    <tr class="total"><td colspan="2">Total (Cash on Delivery)</td><td>₹${total}</td></tr></table>`;
  const d = S.delivery;
  $('dboy').innerHTML = `
    <div class="box info">
      👤 <b>${d.name}</b><br>
      📞 <a href="tel:${d.phone}" style="color:var(--gd);font-weight:600;text-decoration:none">${d.phone}</a><br>
      🏍 Vehicle: ${d.vehicle}<br>
      ⏱ Estimated delivery: <b>${d.eta}</b><br>
      💵 Pay <b>₹${total}</b> in cash on delivery
    </div>
    <p class="tiny" style="margin-top:0">Delivery boy details sample data. Real rider details backend nundi vastayi.</p>`;
}
function placeOrder(){
  if(!S.order.length || !S.loc) return fail('err5',"No items / area selected. Back ki velli select cheyandi.");
  const n=$('oname').value.trim(), p=$('ophone').value.trim(), a=$('oaddr').value.trim();
  if(!n) return fail('err5',"Please enter name");
  if(!/^[6-9]\d{9}$/.test(p)) return fail('err5',"Enter a valid 10 digit phone number");
  if(a.length<8) return fail('err5',"Please enter full address");
  $('err5').textContent="";
  Object.assign(S,{name:n, phone:p, address:a});
  S.orderId = S.preview;
  $('orderidline').innerHTML = `🧾 Order ID: <b>${S.orderId}</b> · Status: <b>Confirmed ✅</b>`;
  $('ordermsg').innerHTML = `<div class="box info">✅ Order placed! ${S.shop.n} (📞 ${S.shop.p}) mimmalni contact chestaru. Delivery boy <b>${S.delivery.name}</b> mee address ki vastaru.</div>`;
  $('placeBtn').disabled = true; $('placeBtn').textContent="Order Placed ✔";
  return true;
}
/* Continue on the bill page: place the order if not placed yet, then open the last page */
function continueFromBill(){
  if(S.order.length && !S.orderId && !placeOrder()) return;
  go(6);
}
function renderFinal(){
  if(!S.orderId){ $('finalsum').innerHTML=""; return; }
  $('finalsum').innerHTML = `<div class="box info">✅ Order <b>${S.orderId}</b> confirmed. Delivery boy <b>${S.delivery.name}</b> (📞 ${S.delivery.phone}) ${S.delivery.eta} lo vastaru.</div>`;
}

/* ================= PAGE 6 ================= */
$('stars').innerHTML = [1,2,3,4,5].map(i=>`<span data-i="${i}">★</span>`).join('');
$('stars').addEventListener('click', e=>{
  if(!e.target.dataset.i) return;
  S.rating = +e.target.dataset.i;
  document.querySelectorAll('#stars span').forEach(s=>s.classList.toggle('on', +s.dataset.i<=S.rating));
});
function sendFeedback(){
  if(!S.rating) return $('fbmsg').textContent="Please give a star rating";
  const fb = {rating:S.rating, feedback:$('fb').value.trim(), date:new Date().toISOString()};
  try { const all=JSON.parse(localStorage.getItem('ss_feedback')||'[]'); all.push(fb); localStorage.setItem('ss_feedback',JSON.stringify(all)); } catch(e){}
  $('fbmsg').style.color='var(--gd)'; $('fbmsg').textContent="Thank you for your feedback! 😊";
}
function closeApp(){
  window.close();
  document.querySelector('.app').innerHTML = '<div class="page active center"><div class="logo">💊</div><h2>SS Medicine Suggestion &amp; Online Orders</h2><p>Visit again! Stay healthy 🌿</p><div class="btns"><button class="primary" onclick="location.reload()">Open Again</button></div></div>';
}
</script>
</body>
</html>
