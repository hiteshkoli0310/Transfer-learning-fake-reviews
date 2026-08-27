# Adding comments and markdown to notebook

**Session ID:** ses_fbc953d71ffeHHlWge7GNQYIRx
**Created:** 8/27/2026, 7:01:05 PM
**Updated:** 8/28/2026, 12:39:24 AM

---

## User

help me document the notebook not too heavy but not to like i want to add comments and markdowns so its much more understanding 

---

## Assistant (Plan · MiMo V2.5 Free · 5.1s)

_Thinking:_

The user wants me to help document a notebook by adding comments and markdown cells to make it more understandable. Let me first find the notebook file(s) in the repository.

**Tool: glob**

**Input:**
```json
{
  "pattern": "**/*.ipynb"
}
```

**Output:**
```
/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/classical model-set-project.ipynb
/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb
```

---

## Assistant (Plan · MiMo V2.5 Free · 28.8s)

_Thinking:_

There are two notebooks. Let me read both to understand their content before making a plan. I should ask the user which notebook they want to document, or if they want both.

I see two notebooks in the repo. Which one(s) do you want me to document?

**Tool: question**

**Input:**
```json
{
  "questions": [
    {
      "question": "Which notebook(s) should I add comments and markdown to?",
      "header": "Notebook selection",
      "options": [
        {
          "label": "classical model-set-project.ipynb",
          "description": "The classical ML models notebook"
        },
        {
          "label": "cross-domain-V2.ipynb",
          "description": "The cross-domain fake review detection notebook"
        },
        {
          "label": "Both notebooks",
          "description": "Document both notebooks"
        }
      ]
    }
  ]
}
```

**Output:**
```
User has answered your questions: "Which notebook(s) should I add comments and markdown to?"="cross-domain-V2.ipynb". You can now continue with the user's answers in mind.
```

---

## Assistant (Plan · MiMo V2.5 Free · 3.6s)

_Thinking:_

The user wants me to document the `cross-domain-V2.ipynb` notebook. Let me read it to understand its structure and content before making a plan.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb"
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
1: {
2:  "cells": [
3:   {
4:    "cell_type": "code",
5:    "execution_count": 226,
6:    "id": "ceb271b9",
7:    "metadata": {},
8:    "outputs": [
9:     {
10:      "name": "stdout",
11:      "output_type": "stream",
12:      "text": [
13:       "Amazon shape: (40432, 4)\n",
14:       "Yelp shape: (359052, 6)\n"
15:      ]
16:     }
17:    ],
18:    "source": [
19:     "import pandas as pd\n",
20:     "import numpy as np\n",
21:     "import re\n",
22:     "from sklearn.utils import resample\n",
23:     "from sklearn.model_selection import train_test_split\n",
24:     "from sklearn.metrics import accuracy_score\n",
25:     "import nltk\n",
26:     "from nltk.corpus import stopwords\n",
27:     "from nltk.stem import PorterStemmer\n",
28:     "\n",
29:     "# Load datasets\n",
30:     "amazon_df = pd.read_csv('fake reviews dataset.csv')\n",
31:     "yelp_df = pd.read_csv('Labelled Yelp Dataset.csv')\n",
32:     "\n",
33:     "# Quick view\n",
34:     "print(\"Amazon shape:\", amazon_df.shape)\n",
35:     "print(\"Yelp shape:\", yelp_df.shape)\n"
36:    ]
37:   },
38:   {
39:    "cell_type": "code",
40:    "execution_count": 227,
41:    "id": "aa9d3b06",
42:    "metadata": {},
43:    "outputs": [],
44:    "source": [
45:     "pd.set_option(\"display.max_columns\", None)\n",
46:     "pd.set_option(\"display.max_colwidth\", 200)"
47:    ]
48:   },
49:   {
50:    "cell_type": "code",
51:    "execution_count": 228,
52:    "id": "55238bc3",
53:    "metadata": {},
54:    "outputs": [
55:     {
56:      "data": {
57:       "text/html": [
58:        "<div>\n",
59:        "<style scoped>\n",
60:        "    .dataframe tbody tr th:only-of-type {\n",
61:        "        vertical-align: middle;\n",
62:        "    }\n",
63:        "\n",
64:        "    .dataframe tbody tr th {\n",
65:        "        vertical-align: top;\n",
66:        "    }\n",
67:        "\n",
68:        "    .dataframe thead th {\n",
69:        "        text-align: right;\n",
70:        "    }\n",
71:        "</style>\n",
72:        "<table border=\"1\" class=\"dataframe\">\n",
73:        "  <thead>\n",
74:        "    <tr style=\"text-align: right;\">\n",
75:        "      <th></th>\n",
76:        "      <th>category</th>\n",
77:        "      <th>rating</th>\n",
78:        "      <th>label</th>\n",
79:        "      <th>text_</th>\n",
80:        "    </tr>\n",
81:        "  </thead>\n",
82:        "  <tbody>\n",
83:        "    <tr>\n",
84:        "      <th>0</th>\n",
85:        "      <td>Home_and_Kitchen_5</td>\n",
86:        "      <td>5.0</td>\n",
87:        "      <td>CG</td>\n",
88:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
89:        "    </tr>\n",
90:        "    <tr>\n",
91:        "      <th>1</th>\n",
92:        "      <td>Home_and_Kitchen_5</td>\n",
93:        "      <td>5.0</td>\n",
94:        "      <td>CG</td>\n",
95:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
96:        "    </tr>\n",
97:        "    <tr>\n",
98:        "      <th>2</th>\n",
99:        "      <td>Home_and_Kitchen_5</td>\n",
100:        "      <td>5.0</td>\n",
101:        "      <td>CG</td>\n",
102:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
103:        "    </tr>\n",
104:        "    <tr>\n",
105:        "      <th>3</th>\n",
106:        "      <td>Home_and_Kitchen_5</td>\n",
107:        "      <td>1.0</td>\n",
108:        "      <td>CG</td>\n",
109:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
110:        "    </tr>\n",
111:        "    <tr>\n",
112:        "      <th>4</th>\n",
113:        "      <td>Home_and_Kitchen_5</td>\n",
114:        "      <td>5.0</td>\n",
115:        "      <td>CG</td>\n",
116:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
117:        "    </tr>\n",
118:        "  </tbody>\n",
119:        "</table>\n",
120:        "</div>"
121:       ],
122:       "text/plain": [
123:        "             category  rating label  \\\n",
124:        "0  Home_and_Kitchen_5     5.0    CG   \n",
125:        "1  Home_and_Kitchen_5     5.0    CG   \n",
126:        "2  Home_and_Kitchen_5     5.0    CG   \n",
127:        "3  Home_and_Kitchen_5     1.0    CG   \n",
128:        "4  Home_and_Kitchen_5     5.0    CG   \n",
129:        "\n",
130:        "                                                                                   text_  \n",
131:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty  \n",
132:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years  \n",
133:        "2                    This pillow saved my back. I love the look and feel of this pillow.  \n",
134:        "3      Missing information on how to use it, but it is a great product for the price!  I  \n",
135:        "4  Very nice set. Good quality. We have had the set for two months now and have not been  "
136:       ]
137:      },
138:      "execution_count": 228,
139:      "metadata": {},
140:      "output_type": "execute_result"
141:     }
142:    ],
143:    "source": [
144:     "amazon_df.head()"
145:    ]
146:   },
147:   {
148:    "cell_type": "code",
149:    "execution_count": 229,
150:    "id": "7800c77e",
151:    "metadata": {},
152:    "outputs": [
153:     {
154:      "data": {
155:       "text/html": [
156:        "<div>\n",
157:        "<style scoped>\n",
158:        "    .dataframe tbody tr th:only-of-type {\n",
159:        "        vertical-align: middle;\n",
160:        "    }\n",
161:        "\n",
162:        "    .dataframe tbody tr th {\n",
163:        "        vertical-align: top;\n",
164:        "    }\n",
165:        "\n",
166:        "    .dataframe thead th {\n",
167:        "        text-align: right;\n",
168:        "    }\n",
169:        "</style>\n",
170:        "<table border=\"1\" class=\"dataframe\">\n",
171:        "  <thead>\n",
172:        "    <tr style=\"text-align: right;\">\n",
173:        "      <th></th>\n",
174:        "      <th>User_id</th>\n",
175:        "      <th>Product_id</th>\n",
176:        "      <th>Rating</th>\n",
177:        "      <th>Date</th>\n",
178:        "      <th>Review</th>\n",
179:        "      <th>Label</th>\n",
180:        "    </tr>\n",
181:        "  </thead>\n",
182:        "  <tbody>\n",
183:        "    <tr>\n",
184:        "      <th>0</th>\n",
185:        "      <td>923</td>\n",
186:        "      <td>0</td>\n",
187:        "      <td>3</td>\n",
188:        "      <td>12/8/2014</td>\n",
189:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
190:        "      <td>-1</td>\n",
191:        "    </tr>\n",
192:        "    <tr>\n",
193:        "      <th>1</th>\n",
194:        "      <td>924</td>\n",
195:        "      <td>0</td>\n",
196:        "      <td>3</td>\n",
197:        "      <td>5/16/2013</td>\n",
198:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
199:        "      <td>-1</td>\n",
200:        "    </tr>\n",
201:        "    <tr>\n",
202:        "      <th>2</th>\n",
203:        "      <td>925</td>\n",
204:        "      <td>0</td>\n",
205:        "      <td>4</td>\n",
206:        "      <td>7/1/2013</td>\n",
207:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
208:        "      <td>-1</td>\n",
209:        "    </tr>\n",
210:        "    <tr>\n",
211:        "      <th>3</th>\n",
212:        "      <td>926</td>\n",
213:        "      <td>0</td>\n",
214:        "      <td>4</td>\n",
215:        "      <td>7/28/2011</td>\n",
216:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
217:        "      <td>-1</td>\n",
218:        "    </tr>\n",
219:        "    <tr>\n",
220:        "      <th>4</th>\n",
221:        "      <td>927</td>\n",
222:        "      <td>0</td>\n",
223:        "      <td>4</td>\n",
224:        "      <td>11/1/2010</td>\n",
225:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
226:        "      <td>-1</td>\n",
227:        "    </tr>\n",
228:        "  </tbody>\n",
229:        "</table>\n",
230:        "</div>"
231:       ],
232:       "text/plain": [
233:        "   User_id  Product_id  Rating       Date  \\\n",
234:        "0      923           0       3  12/8/2014   \n",
235:        "1      924           0       3  5/16/2013   \n",
236:        "2      925           0       4   7/1/2013   \n",
237:        "3      926           0       4  7/28/2011   \n",
238:        "4      927           0       4  11/1/2010   \n",
239:        "\n",
240:        "                                                                                                                                                                                                    Review  \\\n",
241:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
242:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
243:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
244:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
245:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
246:        "\n",
247:        "   Label  \n",
248:        "0     -1  \n",
249:        "1     -1  \n",
250:        "2     -1  \n",
251:        "3     -1  \n",
252:        "4     -1  "
253:       ]
254:      },
255:      "execution_count": 229,
256:      "metadata": {},
257:      "output_type": "execute_result"
258:     }
259:    ],
260:    "source": [
261:     "yelp_df.head()"
262:    ]
263:   },
264:   {
265:    "cell_type": "code",
266:    "execution_count": 230,
267:    "id": "9af9b883",
268:    "metadata": {},
269:    "outputs": [
270:     {
271:      "name": "stdout",
272:      "output_type": "stream",
273:      "text": [
274:       "Column Names:\n",
275:       "\n",
276:       "['category', 'rating', 'label', 'text_']\n",
277:       "\n",
278:       "Dataset Info:\n",
279:       "\n",
280:       "<class 'pandas.DataFrame'>\n",
281:       "RangeIndex: 40432 entries, 0 to 40431\n",
282:       "Data columns (total 4 columns):\n",
283:       " #   Column    Non-Null Count  Dtype  \n",
284:       "---  ------    --------------  -----  \n",
285:       " 0   category  40432 non-null  str    \n",
286:       " 1   rating    40432 non-null  float64\n",
287:       " 2   label     40432 non-null  str    \n",
288:       " 3   text_     40432 non-null  str    \n",
289:       "dtypes: float64(1), str(3)\n",
290:       "memory usage: 15.5 MB\n",
291:       "\n",
292:       "Missing Values:\n",
293:       "\n",
294:       "category    0\n",
295:       "rating      0\n",
296:       "label       0\n",
297:       "text_       0\n",
298:       "dtype: int64\n"
299:      ]
300:     }
301:    ],
302:    "source": [
303:     "print(\"Column Names:\\n\")\n",
304:     "print(amazon_df.columns.tolist())\n",
305:     "\n",
306:     "print(\"\\nDataset Info:\\n\")\n",
307:     "amazon_df.info()\n",
308:     "\n",
309:     "print(\"\\nMissing Values:\\n\")\n",
310:     "print(amazon_df.isnull().sum())"
311:    ]
312:   },
313:   {
314:    "cell_type": "code",
315:    "execution_count": 231,
316:    "id": "f9678399",
317:    "metadata": {},
318:    "outputs": [
319:     {
320:      "name": "stdout",
321:      "output_type": "stream",
322:      "text": [
323:       "Column Names:\n",
324:       "\n",
325:       "['User_id', 'Product_id', 'Rating', 'Date', 'Review', 'Label']\n",
326:       "\n",
327:       "Dataset Info:\n",
328:       "\n",
329:       "<class 'pandas.DataFrame'>\n",
330:       "RangeIndex: 359052 entries, 0 to 359051\n",
331:       "Data columns (total 6 columns):\n",
332:       " #   Column      Non-Null Count   Dtype\n",
333:       "---  ------      --------------   -----\n",
334:       " 0   User_id     359052 non-null  int64\n",
335:       " 1   Product_id  359052 non-null  int64\n",
336:       " 2   Rating      359052 non-null  int64\n",
337:       " 3   Date        359052 non-null  str  \n",
338:       " 4   Review      359052 non-null  str  \n",
339:       " 5   Label       359052 non-null  int64\n",
340:       "dtypes: int64(4), str(2)\n",
341:       "memory usage: 239.0 MB\n",
342:       "\n",
343:       "Missing Values:\n",
344:       "\n",
345:       "User_id       0\n",
346:       "Product_id    0\n",
347:       "Rating        0\n",
348:       "Date          0\n",
349:       "Review        0\n",
350:       "Label         0\n",
351:       "dtype: int64\n"
352:      ]
353:     }
354:    ],
355:    "source": [
356:     "print(\"Column Names:\\n\")\n",
357:     "print(yelp_df.columns.tolist())\n",
358:     "\n",
359:     "print(\"\\nDataset Info:\\n\")\n",
360:     "yelp_df.info()\n",
361:     "\n",
362:     "print(\"\\nMissing Values:\\n\")\n",
363:     "print(yelp_df.isnull().sum())"
364:    ]
365:   },
366:   {
367:    "cell_type": "code",
368:    "execution_count": 232,
369:    "id": "d9a08569",
370:    "metadata": {},
371:    "outputs": [
372:     {
373:      "data": {
374:       "text/html": [
375:        "<div>\n",
376:        "<style scoped>\n",
377:        "    .dataframe tbody tr th:only-of-type {\n",
378:        "        vertical-align: middle;\n",
379:        "    }\n",
380:        "\n",
381:        "    .dataframe tbody tr th {\n",
382:        "        vertical-align: top;\n",
383:        "    }\n",
384:        "\n",
385:        "    .dataframe thead th {\n",
386:        "        text-align: right;\n",
387:        "    }\n",
388:        "</style>\n",
389:        "<table border=\"1\" class=\"dataframe\">\n",
390:        "  <thead>\n",
391:        "    <tr style=\"text-align: right;\">\n",
392:        "      <th></th>\n",
393:        "      <th>category</th>\n",
394:        "      <th>rating</th>\n",
395:        "      <th>label</th>\n",
396:        "      <th>text_</th>\n",
397:        "    </tr>\n",
398:        "  </thead>\n",
399:        "  <tbody>\n",
400:        "    <tr>\n",
401:        "      <th>0</th>\n",
402:        "      <td>Home_and_Kitchen_5</td>\n",
403:        "      <td>5.0</td>\n",
404:        "      <td>1</td>\n",
405:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
406:        "    </tr>\n",
407:        "    <tr>\n",
408:        "      <th>1</th>\n",
409:        "      <td>Home_and_Kitchen_5</td>\n",
410:        "      <td>5.0</td>\n",
411:        "      <td>1</td>\n",
412:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
413:        "    </tr>\n",
414:        "    <tr>\n",
415:        "      <th>2</th>\n",
416:        "      <td>Home_and_Kitchen_5</td>\n",
417:        "      <td>5.0</td>\n",
418:        "      <td>1</td>\n",
419:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
420:        "    </tr>\n",
421:        "    <tr>\n",
422:        "      <th>3</th>\n",
423:        "      <td>Home_and_Kitchen_5</td>\n",
424:        "      <td>1.0</td>\n",
425:        "      <td>1</td>\n",
426:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
427:        "    </tr>\n",
428:        "    <tr>\n",
429:        "      <th>4</th>\n",
430:        "      <td>Home_and_Kitchen_5</td>\n",
431:        "      <td>5.0</td>\n",
432:        "      <td>1</td>\n",
433:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
434:        "    </tr>\n",
435:        "  </tbody>\n",
436:        "</table>\n",
437:        "</div>"
438:       ],
439:       "text/plain": [
440:        "             category  rating  label  \\\n",
441:        "0  Home_and_Kitchen_5     5.0      1   \n",
442:        "1  Home_and_Kitchen_5     5.0      1   \n",
443:        "2  Home_and_Kitchen_5     5.0      1   \n",
444:        "3  Home_and_Kitchen_5     1.0      1   \n",
445:        "4  Home_and_Kitchen_5     5.0      1   \n",
446:        "\n",
447:        "                                                                                   text_  \n",
448:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty  \n",
449:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years  \n",
450:        "2                    This pillow saved my back. I love the look and feel of this pillow.  \n",
451:        "3      Missing information on how to use it, but it is a great product for the price!  I  \n",
452:        "4  Very nice set. Good quality. We have had the set for two months now and have not been  "
453:       ]
454:      },
455:      "execution_count": 232,
456:      "metadata": {},
457:      "output_type": "execute_result"
458:     }
459:    ],
460:    "source": [
461:     "label_map={'CG':1,'OR':0}\n",
462:     "amazon_df['label']=amazon_df['label'].map(label_map)\n",
463:     "amazon_df.head()"
464:    ]
465:   },
466:   {
467:    "cell_type": "code",
468:    "execution_count": 233,
469:    "id": "489d777d",
470:    "metadata": {},
471:    "outputs": [
472:     {
473:      "data": {
474:       "text/html": [
475:        "<div>\n",
476:        "<style scoped>\n",
477:        "    .dataframe tbody tr th:only-of-type {\n",
478:        "        vertical-align: middle;\n",
479:        "    }\n",
480:        "\n",
481:        "    .dataframe tbody tr th {\n",
482:        "        vertical-align: top;\n",
483:        "    }\n",
484:        "\n",
485:        "    .dataframe thead th {\n",
486:        "        text-align: right;\n",
487:        "    }\n",
488:        "</style>\n",
489:        "<table border=\"1\" class=\"dataframe\">\n",
490:        "  <thead>\n",
491:        "    <tr style=\"text-align: right;\">\n",
492:        "      <th></th>\n",
493:        "      <th>rating</th>\n",
494:        "      <th>review</th>\n",
495:        "      <th>label</th>\n",
496:        "    </tr>\n",
497:        "  </thead>\n",
498:        "  <tbody>\n",
499:        "    <tr>\n",
500:        "      <th>0</th>\n",
501:        "      <td>5.0</td>\n",
502:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
503:        "      <td>1</td>\n",
504:        "    </tr>\n",
505:        "    <tr>\n",
506:        "      <th>1</th>\n",
507:        "      <td>5.0</td>\n",
508:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
509:        "      <td>1</td>\n",
510:        "    </tr>\n",
511:        "    <tr>\n",
512:        "      <th>2</th>\n",
513:        "      <td>5.0</td>\n",
514:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
515:        "      <td>1</td>\n",
516:        "    </tr>\n",
517:        "    <tr>\n",
518:        "      <th>3</th>\n",
519:        "      <td>1.0</td>\n",
520:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
521:        "      <td>1</td>\n",
522:        "    </tr>\n",
523:        "    <tr>\n",
524:        "      <th>4</th>\n",
525:        "      <td>5.0</td>\n",
526:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
527:        "      <td>1</td>\n",
528:        "    </tr>\n",
529:        "  </tbody>\n",
530:        "</table>\n",
531:        "</div>"
532:       ],
533:       "text/plain": [
534:        "   rating  \\\n",
535:        "0     5.0   \n",
536:        "1     5.0   \n",
537:        "2     5.0   \n",
538:        "3     1.0   \n",
539:        "4     5.0   \n",
540:        "\n",
541:        "                                                                                  review  \\\n",
542:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty   \n",
543:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years   \n",
544:        "2                    This pillow saved my back. I love the look and feel of this pillow.   \n",
545:        "3      Missing information on how to use it, but it is a great product for the price!  I   \n",
546:        "4  Very nice set. Good quality. We have had the set for two months now and have not been   \n",
547:        "\n",
548:        "   label  \n",
549:        "0      1  \n",
550:        "1      1  \n",
551:        "2      1  \n",
552:        "3      1  \n",
553:        "4      1  "
554:       ]
555:      },
556:      "execution_count": 233,
557:      "metadata": {},
558:      "output_type": "execute_result"
559:     }
560:    ],
561:    "source": [
562:     "#Amazon rename and remove unwanted columns\n",
563:     "\n",
564:     "amazon_df = amazon_df.rename(columns={\n",
565:     "    \"text_\": \"review\"\n",
566:     "})\n",
567:     "\n",
568:     "amazon_df = amazon_df[[\"rating\",\"review\",\"label\"]]\n",
569:     "\n",
570:     "amazon_df.head()"
571:    ]
572:   },
573:   {
574:    "cell_type": "code",
575:    "execution_count": 234,
576:    "id": "a652d43b",
577:    "metadata": {},
578:    "outputs": [
579:     {
580:      "data": {
581:       "text/html": [
582:        "<div>\n",
583:        "<style scoped>\n",
584:        "    .dataframe tbody tr th:only-of-type {\n",
585:        "        vertical-align: middle;\n",
586:        "    }\n",
587:        "\n",
588:        "    .dataframe tbody tr th {\n",
589:        "        vertical-align: top;\n",
590:        "    }\n",
591:        "\n",
592:        "    .dataframe thead th {\n",
593:        "        text-align: right;\n",
594:        "    }\n",
595:        "</style>\n",
596:        "<table border=\"1\" class=\"dataframe\">\n",
597:        "  <thead>\n",
598:        "    <tr style=\"text-align: right;\">\n",
599:        "      <th></th>\n",
600:        "      <th>rating</th>\n",
601:        "      <th>review</th>\n",
602:        "      <th>label</th>\n",
603:        "    </tr>\n",
604:        "  </thead>\n",
605:        "  <tbody>\n",
606:        "    <tr>\n",
607:        "      <th>0</th>\n",
608:        "      <td>3</td>\n",
609:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
610:        "      <td>-1</td>\n",
611:        "    </tr>\n",
612:        "    <tr>\n",
613:        "      <th>1</th>\n",
614:        "      <td>3</td>\n",
615:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
616:        "      <td>-1</td>\n",
617:        "    </tr>\n",
618:        "    <tr>\n",
619:        "      <th>2</th>\n",
620:        "      <td>4</td>\n",
621:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
622:        "      <td>-1</td>\n",
623:        "    </tr>\n",
624:        "    <tr>\n",
625:        "      <th>3</th>\n",
626:        "      <td>4</td>\n",
627:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
628:        "      <td>-1</td>\n",
629:        "    </tr>\n",
630:        "    <tr>\n",
631:        "      <th>4</th>\n",
632:        "      <td>4</td>\n",
633:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
634:        "      <td>-1</td>\n",
635:        "    </tr>\n",
636:        "  </tbody>\n",
637:        "</table>\n",
638:        "</div>"
639:       ],
640:       "text/plain": [
641:        "   rating  \\\n",
642:        "0       3   \n",
643:        "1       3   \n",
644:        "2       4   \n",
645:        "3       4   \n",
646:        "4       4   \n",
647:        "\n",
648:        "                                                                                                                                                                                                    review  \\\n",
649:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
650:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
651:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
652:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
653:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
654:        "\n",
655:        "   label  \n",
656:        "0     -1  \n",
657:        "1     -1  \n",
658:        "2     -1  \n",
659:        "3     -1  \n",
660:        "4     -1  "
661:       ]
662:      },
663:      "execution_count": 234,
664:      "metadata": {},
665:      "output_type": "execute_result"
666:     }
667:    ],
668:    "source": [
669:     "#Yelp rename and remove unwanted columns\n",
670:     "\n",
671:     "yelp_df=yelp_df.rename(columns={\n",
672:     "    \"Rating\":\"rating\",\n",
673:     "    \"Review\":\"review\",\n",
674:     "    \"Label\":\"label\"\n",
675:     "})\n",
676:     "\n",
677:     "yelp_df=yelp_df[[\"rating\",\"review\",\"label\"]]\n",
678:     "\n",
679:     "yelp_df.head()"
680:    ]
681:   },
682:   {
683:    "cell_type": "code",
684:    "execution_count": 235,
685:    "id": "23166f6e",
686:    "metadata": {},
687:    "outputs": [
688:     {
689:      "data": {
690:       "text/html": [
691:        "<div>\n",
692:        "<style scoped>\n",
693:        "    .dataframe tbody tr th:only-of-type {\n",
694:        "        vertical-align: middle;\n",
695:        "    }\n",
696:        "\n",
697:        "    .dataframe tbody tr th {\n",
698:        "        vertical-align: top;\n",
699:        "    }\n",
700:        "\n",
701:        "    .dataframe thead th {\n",
702:        "        text-align: right;\n",
703:        "    }\n",
704:        "</style>\n",
705:        "<table border=\"1\" class=\"dataframe\">\n",
706:        "  <thead>\n",
707:        "    <tr style=\"text-align: right;\">\n",
708:        "      <th></th>\n",
709:        "      <th>rating</th>\n",
710:        "      <th>review</th>\n",
711:        "      <th>label</th>\n",
712:        "    </tr>\n",
713:        "  </thead>\n",
714:        "  <tbody>\n",
715:        "    <tr>\n",
716:        "      <th>0</th>\n",
717:        "      <td>3</td>\n",
718:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
719:        "      <td>1</td>\n",
720:        "    </tr>\n",
721:        "    <tr>\n",
722:        "      <th>1</th>\n",
723:        "      <td>3</td>\n",
724:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
725:        "      <td>1</td>\n",
726:        "    </tr>\n",
727:        "    <tr>\n",
728:        "      <th>2</th>\n",
729:        "      <td>4</td>\n",
730:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
731:        "      <td>1</td>\n",
732:        "    </tr>\n",
733:        "    <tr>\n",
734:        "      <th>3</th>\n",
735:        "      <td>4</td>\n",
736:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
737:        "      <td>1</td>\n",
738:        "    </tr>\n",
739:        "    <tr>\n",
740:        "      <th>4</th>\n",
741:        "      <td>4</td>\n",
742:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
743:        "      <td>1</td>\n",
744:        "    </tr>\n",
745:        "  </tbody>\n",
746:        "</table>\n",
747:        "</div>"
748:       ],
749:       "text/plain": [
750:        "   rating  \\\n",
751:        "0       3   \n",
752:        "1       3   \n",
753:        "2       4   \n",
754:        "3       4   \n",
755:        "4       4   \n",
756:        "\n",
757:        "                                                                                                                                                                                                    review  \\\n",
758:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
759:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
760:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
761:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
762:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
763:        "\n",
764:        "   label  \n",
765:        "0      1  \n",
766:        "1      1  \n",
767:        "2      1  \n",
768:        "3      1  \n",
769:        "4      1  "
770:       ]
771:      },
772:      "execution_count": 235,
773:      "metadata": {},
774:      "output_type": "execute_result"
775:     }
776:    ],
777:    "source": [
778:     "label_map={-1:1,1:0}\n",
779:     "yelp_df['label']=yelp_df['label'].map(label_map)\n",
780:     "yelp_df.head()"
781:    ]
782:   },
783:   {
784:    "cell_type": "code",
785:    "execution_count": 236,
786:    "id": "1e220dea",
787:    "metadata": {},
788:    "outputs": [
789:     {
790:      "name": "stdout",
791:      "output_type": "stream",
792:      "text": [
793:       "<class 'pandas.DataFrame'>\n",
794:       "RangeIndex: 40432 entries, 0 to 40431\n",
795:       "Data columns (total 3 columns):\n",
796:       " #   Column  Non-Null Count  Dtype  \n",
797:       "---  ------  --------------  -----  \n",
798:       " 0   rating  40432 non-null  float64\n",
799:       " 1   review  40432 non-null  str    \n",
800:       " 2   label   40432 non-null  int64  \n",
801:       "dtypes: float64(1), int64(1), str(1)\n",
802:       "memory usage: 14.5 MB\n"
803:      ]
804:     }
805:    ],
806:    "source": [
807:     "amazon_df.info()"
808:    ]
809:   },
810:   {
811:    "cell_type": "code",
812:    "execution_count": 237,
813:    "id": "f27d1399",
814:    "metadata": {},
815:    "outputs": [
816:     {
817:      "data": {
818:       "text/plain": [
819:        "array([5., 1., 3., 2., 4.])"
820:       ]
821:      },
822:      "execution_count": 237,
823:      "metadata": {},
824:      "output_type": "execute_result"
825:     }
826:    ],
827:    "source": [
828:     "amazon_df[\"rating\"].unique()"
829:    ]
830:   },
831:   {
832:    "cell_type": "code",
833:    "execution_count": 238,
834:    "id": "edf61ac9",
835:    "metadata": {},
836:    "outputs": [],
837:    "source": [
838:     "amazon_df[\"rating\"]=amazon_df[\"rating\"].astype(int)"
839:    ]
840:   },
841:   {
842:    "cell_type": "code",
843:    "execution_count": 239,
844:    "id": "7b4ed1e5",
845:    "metadata": {},
846:    "outputs": [
847:     {
848:      "name": "stdout",
849:      "output_type": "stream",
850:      "text": [
851:       "<class 'pandas.DataFrame'>\n",
852:       "RangeIndex: 359052 entries, 0 to 359051\n",
853:       "Data columns (total 3 columns):\n",
854:       " #   Column  Non-Null Count   Dtype\n",
855:       "---  ------  --------------   -----\n",
856:       " 0   rating  359052 non-null  int64\n",
857:       " 1   review  359052 non-null  str  \n",
858:       " 2   label   359052 non-null  int64\n",
859:       "dtypes: int64(2), str(1)\n",
860:       "memory usage: 227.7 MB\n"
861:      ]
862:     }
863:    ],
864:    "source": [
865:     "yelp_df.info()"
866:    ]
867:   },
868:   {
869:    "cell_type": "code",
870:    "execution_count": 240,
871:    "id": "eb911bf5",
872:    "metadata": {},
873:    "outputs": [
874:     {
875:      "name": "stdout",
876:      "output_type": "stream",
877:      "text": [
878:       "Duplicates Before: 12\n"
879:      ]
880:     }
881:    ],
882:    "source": [
883:     "print(\"Duplicates Before:\", amazon_df.duplicated().sum())"
884:    ]
885:   },
886:   {
887:    "cell_type": "code",
888:    "execution_count": 241,
889:    "id": "09285ccc",
890:    "metadata": {},
891:    "outputs": [
892:     {
893:      "name": "stdout",
894:      "output_type": "stream",
895:      "text": [
896:       "Dataset Shape After Removing Duplicates: (40412, 3)\n"
897:      ]
898:     }
899:    ],
900:    "source": [
901:     "amazon_df = amazon_df.drop_duplicates(subset=\"review\").reset_index(drop=True)\n",
902:     "\n",
903:     "print(\"Dataset Shape After Removing Duplicates:\", amazon_df.shape)"
904:    ]
905:   },
906:   {
907:    "cell_type": "code",
908:    "execution_count": 242,
909:    "id": "579a79b2",
910:    "metadata": {},
911:    "outputs": [
912:     {
913:      "name": "stdout",
914:      "output_type": "stream",
915:      "text": [
916:       "Duplicates Before: 469\n"
917:      ]
918:     }
919:    ],
920:    "source": [
921:     "print(\"Duplicates Before:\", yelp_df.duplicated().sum())"
922:    ]
923:   },
924:   {
925:    "cell_type": "code",
926:    "execution_count": 243,
927:    "id": "e16e34e8",
928:    "metadata": {},
929:    "outputs": [
930:     {
931:      "name": "stdout",
932:      "output_type": "stream",
933:      "text": [
934:       "Dataset Shape After Removing Duplicates: (358156, 3)\n"
935:      ]
936:     }
937:    ],
938:    "source": [
939:     "yelp_df = yelp_df.drop_duplicates(subset=\"review\").reset_index(drop=True)\n",
940:     "\n",
941:     "print(\"Dataset Shape After Removing Duplicates:\", yelp_df.shape)"
942:    ]
943:   },
944:   {
945:    "cell_type": "code",
946:    "execution_count": 244,
947:    "id": "2fe0a1b8",
948:    "metadata": {},
949:    "outputs": [],
950:    "source": [
951:     "def count_patterns(df, column):\n",
952:     "    # Convert column to string (ignore NaN issues)\n",
953:     "    text = df[column].fillna(\"\").astype(str)\n",
954:     "\n",
955:     "    html_count = text.str.contains(r\"<.*?>\", regex=True).sum()\n",
956:     "    url_count = text.str.contains(r\"http\\S+|www\\.\\S+\", regex=True).sum()\n",
957:     "    email_count = text.str.contains(r\"\\S+@\\S+\", regex=True).sum()\n",
958:     "\n",
959:     "    print(f\"Total rows: {len(df)}\")\n",
960:     "    print(f\"Rows with HTML tags   : {html_count}\")\n",
961:     "    print(f\"Rows with URLs        : {url_count}\")\n",
962:     "    print(f\"Rows with Email IDs   : {email_count}\")\n",
963:     "\n",
964:     "    return {\n",
965:     "        \"html_tags\": html_count,\n",
966:     "        \"urls\": url_count,\n",
967:     "        \"emails\": email_count\n",
968:     "    }"
969:    ]
970:   },
971:   {
972:    "cell_type": "code",
973:    "execution_count": 245,
974:    "id": "b083f438",
975:    "metadata": {},
976:    "outputs": [
977:     {
978:      "name": "stdout",
979:      "output_type": "stream",
980:      "text": [
981:       "Total rows: 40412\n",
982:       "Rows with HTML tags   : 203\n",
983:       "Rows with URLs        : 109\n",
984:       "Rows with Email IDs   : 11\n",
985:       "{'html_tags': np.int64(203), 'urls': np.int64(109), 'emails': np.int64(11)}\n",
986:       "Total rows: 358156\n",
987:       "Rows with HTML tags   : 0\n",
988:       "Rows with URLs        : 33\n",
989:       "Rows with Email IDs   : 215\n",
990:       "{'html_tags': np.int64(0), 'urls': np.int64(33), 'emails': np.int64(215)}\n"
991:      ]
992:     }
993:    ],
994:    "source": [
995:     "print(count_patterns(amazon_df, \"review\"))\n",
996:     "print(count_patterns(yelp_df, \"review\"))"
997:    ]
998:   },
999:   {
1000:    "cell_type": "code",
1001:    "execution_count": 246,
1002:    "id": "7944a5ba",
1003:    "metadata": {},
1004:    "outputs": [],
1005:    "source": [
1006:     "import html\n",
1007:     "\n",
1008:     "def clean_review(text):\n",
1009:     "    # Convert to string\n",
1010:     "    text = str(text)\n",
1011:     "\n",
1012:     "    # Decode HTML entities\n",
1013:     "    text = html.unescape(text)\n",
1014:     "\n",
1015:     "    # Remove HTML tags\n",
1016:     "    text = re.sub(r\"<.*?>\", \" \", text)\n",
1017:     "\n",
1018:     "    # Remove URLs\n",
1019:     "    text = re.sub(r\"http\\\\S+|www\\\\.\\\\S+\", \" \", text)\n",
1020:     "\n",
1021:     "    # Remove email addresses\n",
1022:     "    text = re.sub(r\"\\\\S+@\\\\S+\", \" \", text)\n",
1023:     "\n",
1024:     "    # Fix common encoding artifacts\n",
1025:     "    text = re.sub(r\"[ÂâÃ]+\", \" \", text)\n",
1026:     "    \n",
1027:     "    # Remove all remaining non-ASCII characters (optional)\n",
1028:     "    text = re.sub(r\"[^\\x00-\\x7F]+\", \" \", text)\n",
1029:     "    \n",
1030:     "    # Remove extra spaces/newlines/tabs\n",
1031:     "    text = re.sub(r\"\\\\s+\", \" \", text).strip()\n",
1032:     "    \n",
1033:     "    # Remove newline, tab, and extra whitespace\n",
1034:     "    text = re.sub(r\"\\s+\", \" \", text).strip()\n",
1035:     "\n",
1036:     "    # Remove special symbols/punctuation and replace with a space\n",
1037:     "    text = re.sub(r\"[^\\w\\s]\", \" \", text)\n",
1038:     "\n",
1039:     "    # Collapse multiple spaces created after removing symbols\n",
1040:     "    text = re.sub(r\"\\s+\", \" \", text).strip()\n",
1041:     "    \n",
1042:     "    # Lowercase only\n",
1043:     "    text = text.lower()\n",
1044:     "\n",
1045:     "    return text"
1046:    ]
1047:   },
1048:   {
1049:    "cell_type": "code",
1050:    "execution_count": 247,
1051:    "id": "3f8701e8",
1052:    "metadata": {},
1053:    "outputs": [],
1054:    "source": [
1055:     "amazon_df[\"review\"] = amazon_df[\"review\"].apply(clean_review)"
1056:    ]
1057:   },
1058:   {
1059:    "cell_type": "code",
1060:    "execution_count": 248,
1061:    "id": "6bd5c901",
1062:    "metadata": {},
1063:    "outputs": [],
1064:    "source": [
1065:     "yelp_df[\"review\"] = yelp_df[\"review\"].apply(clean_review)"
1066:    ]
1067:   },
1068:   {
1069:    "cell_type": "code",
1070:    "execution_count": 249,
1071:    "id": "d0355a58",
1072:    "metadata": {},
1073:    "outputs": [
1074:     {
1075:      "name": "stdout",
1076:      "output_type": "stream",
1077:      "text": [
1078:       "Dataset Shape: (40411, 3)\n"
1079:      ]
1080:     }
1081:    ],
1082:    "source": [
1083:     "amazon_df = amazon_df[amazon_df[\"review\"].str.len() > 0].reset_index(drop=True)\n",
1084:     "\n",
1085:     "print(\"Dataset Shape:\", amazon_df.shape)"
1086:    ]
1087:   },
1088:   {
1089:    "cell_type": "code",
1090:    "execution_count": 250,
1091:    "id": "b3467bac",
1092:    "metadata": {},
1093:    "outputs": [
1094:     {
1095:      "name": "stdout",
1096:      "output_type": "stream",
1097:      "text": [
1098:       "Dataset Shape: (358142, 3)\n"
1099:      ]
1100:     }
1101:    ],
1102:    "source": [
1103:     "yelp_df = yelp_df[yelp_df[\"review\"].str.len() > 0].reset_index(drop=True)\n",
1104:     "\n",
1105:     "print(\"Dataset Shape:\", yelp_df.shape)"
1106:    ]
1107:   },
1108:   {
1109:    "cell_type": "code",
1110:    "execution_count": 251,
1111:    "id": "1977cd89",
1112:    "metadata": {},
1113:    "outputs": [
1114:     {
1115:      "name": "stdout",
1116:      "output_type": "stream",
1117:      "text": [
1118:       "label\n",
1119:       "0    20215\n",
1120:       "1    20196\n",
1121:       "Name: count, dtype: int64\n",
1122:       "\n",
1123:       "Percentage Distribution:\n",
1124:       "label\n",
1125:       "0    50.02\n",
1126:       "1    49.98\n",
1127:       "Name: count, dtype: float64\n"
1128:      ]
1129:     }
1130:    ],
1131:    "source": [
1132:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
1133:     "\n",
1134:     "print(label_counts)\n",
1135:     "\n",
1136:     "print(\"\\nPercentage Distribution:\")\n",
1137:     "print((label_counts / len(amazon_df) * 100).round(2))"
1138:    ]
1139:   },
1140:   {
1141:    "cell_type": "code",
1142:    "execution_count": 252,
1143:    "id": "c83f6a6e",
1144:    "metadata": {},
1145:    "outputs": [
1146:     {
1147:      "name": "stdout",
1148:      "output_type": "stream",
1149:      "text": [
1150:       "label\n",
1151:       "0    321568\n",
1152:       "1     36574\n",
1153:       "Name: count, dtype: int64\n",
1154:       "\n",
1155:       "Percentage Distribution:\n",
1156:       "label\n",
1157:       "0    89.79\n",
1158:       "1    10.21\n",
1159:       "Name: count, dtype: float64\n"
1160:      ]
1161:     }
1162:    ],
1163:    "source": [
1164:     "label_counts = yelp_df[\"label\"].value_counts().sort_index()\n",
1165:     "\n",
1166:     "print(label_counts)\n",
1167:     "\n",
1168:     "print(\"\\nPercentage Distribution:\")\n",
1169:     "print((label_counts / len(yelp_df) * 100).round(2))"
1170:    ]
1171:   },
1172:   {
1173:    "cell_type": "code",
1174:    "execution_count": 253,
1175:    "id": "3bdf9942",
1176:    "metadata": {},
1177:    "outputs": [
1178:     {
1179:      "name": "stdout",
1180:      "output_type": "stream",
1181:      "text": [
1182:       "Label counts:\n",
1183:       " label\n",
1184:       "1    25000\n",
1185:       "0    25000\n",
1186:       "Name: count, dtype: int64\n"
1187:      ]
1188:     }
1189:    ],
1190:    "source": [
1191:     "fake = yelp_df[yelp_df['label'] == 0].sample(n=25000, random_state=42)\n",
1192:     "real = yelp_df[yelp_df['label'] == 1].sample(n=25000, random_state=42)\n",
1193:     "\n",
1194:     "yelp_sample = (\n",
1195:     "    pd.concat([fake, real])\n",
1196:     "      .sample(frac=1, random_state=42)   # shuffle\n",
1197:     "      .reset_index(drop=True)\n",
1198:     ")\n",
1199:     "print(\"Label counts:\\n\", yelp_sample['label'].value_counts())"
1200:    ]
1201:   },
1202:   {
1203:    "cell_type": "code",
1204:    "execution_count": 254,
1205:    "id": "f29b9a60",
1206:    "metadata": {},
1207:    "outputs": [
1208:     {
1209:      "name": "stdout",
1210:      "output_type": "stream",
1211:      "text": [
1212:       "Label counts:\n",
1213:       " label\n",
1214:       "0    20215\n",
1215:       "1    20196\n",
1216:       "Name: count, dtype: int64\n"
1217:      ]
1218:     }
1219:    ],
1220:    "source": [
1221:     "print(\"Label counts:\\n\", amazon_df['label'].value_counts())"
1222:    ]
1223:   },
1224:   {
1225:    "cell_type": "code",
1226:    "execution_count": 255,
1227:    "id": "1c3c0c8d",
1228:    "metadata": {},
1229:    "outputs": [
1230:     {
1231:      "name": "stdout",
1232:      "output_type": "stream",
1233:      "text": [
1234:       "Empty Reviews : 0\n",
1235:       "Average Review Length : 339.90292247160426\n",
1236:       "Shortest Review Length : 4\n",
1237:       "Longest Review Length : 2095\n"
1238:      ]
1239:     }
1240:    ],
1241:    "source": [
1242:     "#amazon\n",
1243:     "\n",
1244:     "print(\"Empty Reviews :\", (amazon_df[\"review\"] == \"\").sum())\n",
1245:     "\n",
1246:     "print(\"Average Review Length :\", amazon_df[\"review\"].str.len().mean())\n",
1247:     "\n",
1248:     "print(\"Shortest Review Length :\", amazon_df[\"review\"].str.len().min())\n",
1249:     "\n",
1250:     "print(\"Longest Review Length :\", amazon_df[\"review\"].str.len().max())"
1251:    ]
1252:   },
1253:   {
1254:    "cell_type": "code",
1255:    "execution_count": 256,
1256:    "id": "f5bf54a4",
1257:    "metadata": {},
1258:    "outputs": [
1259:     {
1260:      "data": {
1261:       "text/html": [
1262:        "<div>\n",
1263:        "<style scoped>\n",
1264:        "    .dataframe tbody tr th:only-of-type {\n",
1265:        "        vertical-align: middle;\n",
1266:        "    }\n",
1267:        "\n",
1268:        "    .dataframe tbody tr th {\n",
1269:        "        vertical-align: top;\n",
1270:        "    }\n",
1271:        "\n",
1272:        "    .dataframe thead th {\n",
1273:        "        text-align: right;\n",
1274:        "    }\n",
1275:        "</style>\n",
1276:        "<table border=\"1\" class=\"dataframe\">\n",
1277:        "  <thead>\n",
1278:        "    <tr style=\"text-align: right;\">\n",
1279:        "      <th></th>\n",
1280:        "      <th>rating</th>\n",
1281:        "      <th>review</th>\n",
1282:        "      <th>label</th>\n",
1283:        "    </tr>\n",
1284:        "  </thead>\n",
1285:        "  <tbody>\n",
1286:        "    <tr>\n",
1287:        "      <th>9907</th>\n",
1288:        "      <td>5</td>\n",
1289:        "      <td>input</td>\n",
1290:        "      <td>1</td>\n",
1291:        "    </tr>\n",
1292:        "    <tr>\n",
1293:        "      <th>18615</th>\n",
1294:        "      <td>3</td>\n",
1295:        "      <td>pfister lf 042 prcc</td>\n",
1296:        "      <td>1</td>\n",
1297:        "    </tr>\n",
1298:        "    <tr>\n",
1299:        "      <th>21677</th>\n",
1300:        "      <td>5</td>\n",
1301:        "      <td>well</td>\n",
1302:        "      <td>1</td>\n",
1303:        "    </tr>\n",
1304:        "    <tr>\n",
1305:        "      <th>36815</th>\n",
1306:        "      <td>5</td>\n",
1307:        "      <td>nice elegant watch</td>\n",
1308:        "      <td>1</td>\n",
1309:        "    </tr>\n",
1310:        "  </tbody>\n",
1311:        "</table>\n",
1312:        "</div>"
1313:       ],
1314:       "text/plain": [
1315:        "       rating               review  label\n",
1316:        "9907        5                input      1\n",
1317:        "18615       3  pfister lf 042 prcc      1\n",
1318:        "21677       5                 well      1\n",
1319:        "36815       5   nice elegant watch      1"
1320:       ]
1321:      },
1322:      "execution_count": 256,
1323:      "metadata": {},
1324:      "output_type": "execute_result"
1325:     }
1326:    ],
1327:    "source": [
1328:     "# Print rows where text has fewer than 20 characters\n",
1329:     "amazon_df[amazon_df[\"review\"].str.len() < 20]"
1330:    ]
1331:   },
1332:   {
1333:    "cell_type": "code",
1334:    "execution_count": 257,
1335:    "id": "6f0277ef",
1336:    "metadata": {},
1337:    "outputs": [
1338:     {
1339:      "data": {
1340:       "text/html": [
1341:        "<div>\n",
1342:        "<style scoped>\n",
1343:        "    .dataframe tbody tr th:only-of-type {\n",
1344:        "        vertical-align: middle;\n",
1345:        "    }\n",
1346:        "\n",
1347:        "    .dataframe tbody tr th {\n",
1348:        "        vertical-align: top;\n",
1349:        "    }\n",
1350:        "\n",
1351:        "    .dataframe thead th {\n",
1352:        "        text-align: right;\n",
1353:        "    }\n",
1354:        "</style>\n",
1355:        "<table border=\"1\" class=\"dataframe\">\n",
1356:        "  <thead>\n",
1357:        "    <tr style=\"text-align: right;\">\n",
1358:        "      <th></th>\n",
1359:        "      <th>rating</th>\n",
1360:        "      <th>review</th>\n",
1361:        "      <th>label</th>\n",
1362:        "    </tr>\n",
1363:        "  </thead>\n",
1364:        "  <tbody>\n",
1365:        "    <tr>\n",
1366:        "      <th>2410</th>\n",
1367:        "      <td>1</td>\n",
1368:        "      <td>i had a hard time contacting the manufacturer distributor in order to make sure the measurements were correct the description and the pdf have completely different dimensions in reality these didn...</td>\n",
1369:        "      <td>0</td>\n",
1370:        "    </tr>\n",
1371:        "    <tr>\n",
1372:        "      <th>2578</th>\n",
1373:        "      <td>5</td>\n",
1374:        "      <td>i purchased this bed and have slept on it for the past week i believe in trying things out to make sure my guests won t suffer from backaches etc the aerobed provides a comfortable night s rest i ...</td>\n",
1375:        "      <td>0</td>\n",
1376:        "    </tr>\n",
1377:        "    <tr>\n",
1378:        "      <th>2605</th>\n",
1379:        "      <td>4</td>\n",
1380:        "      <td>after my first night sleeping on a neckbone pillow i ordered another one so my husband could have his own too i could already feel improvement in my neck and shoulder problems after just one night...</td>\n",
1381:        "      <td>0</td>\n",
1382:        "    </tr>\n",
1383:        "    <tr>\n",
1384:        "      <th>2608</th>\n",
1385:        "      <td>5</td>\n",
1386:        "      <td>these canisters are the perfect size for us we use the smallest one for powdered creamer the middle size for instant coffee and the largest size for sugar which we use to refill our smaller sugar ...</td>\n",
1387:        "      <td>0</td>\n",
1388:        "    </tr>\n",
1389:        "    <tr>\n",
1390:        "      <th>2637</th>\n",
1391:        "      <td>5</td>\n",
1392:        "      <td>these are really wonderful they are perfect for strawberry hulling neatly and easily i ve owned a dozen not because they wear out they don t they just seem to wander away when i m not looking fort...</td>\n",
1393:        "      <td>0</td>\n",
1394:        "    </tr>\n",
1395:        "    <tr>\n",
1396:        "      <th>...</th>\n",
1397:        "      <td>...</td>\n",
1398:        "      <td>...</td>\n",
1399:        "      <td>...</td>\n",
1400:        "    </tr>\n",
1401:        "    <tr>\n",
1402:        "      <th>40406</th>\n",
1403:        "      <td>4</td>\n",
1404:        "      <td>i had read some reviews saying that this bra ran small and so i ordered two band and cup sizes up and it was still too small definitely along the lines of a sports bra squish effect the sides do c...</td>\n",
1405:        "      <td>0</td>\n",
1406:        "    </tr>\n",
1407:        "    <tr>\n",
1408:        "      <th>40407</th>\n",
1409:        "      <td>5</td>\n",
1410:        "      <td>i wasn t sure exactly what it would be it is a little large for my small size but i think it is a nice fit the fabric is a nice thin material but it is a little thin in the legs i wish it was thic...</td>\n",
1411:        "      <td>1</td>\n",
1412:        "    </tr>\n",
1413:        "    <tr>\n",
1414:        "      <th>40408</th>\n",
1415:        "      <td>2</td>\n",
1416:        "      <td>you can wear the hood by itself wear it with the hood or wear just the jacket without the hood how is that for 3 in 1 systems reminiscent of what lands end sells as a squall jacket or what uniform...</td>\n",
1417:        "      <td>0</td>\n",
1418:        "    </tr>\n",
1419:        "    <tr>\n",
1420:        "      <th>40409</th>\n",
1421:        "      <td>1</td>\n",
1422:        "      <td>i liked nothing about this dress the only reason i gave it 4 stars is because i ordered the size 6 5 and it fit perfectly the fabric is a nice thin material and the color is vibrant it s a little ...</td>\n",
1423:        "      <td>1</td>\n",
1424:        "    </tr>\n",
1425:        "    <tr>\n",
1426:        "      <th>40410</th>\n",
1427:        "      <td>5</td>\n",
1428:        "      <td>i work in the wedding industry and have to work long days on my feet outside in the heat and have to look professional i ve spent a ridiculous amount of money on high end dress shoes like merrels ...</td>\n",
1429:        "      <td>0</td>\n",
1430:        "    </tr>\n",
1431:        "  </tbody>\n",
1432:        "</table>\n",
1433:        "<p>14050 rows × 3 columns</p>\n",
1434:        "</div>"
1435:       ],
1436:       "text/plain": [
1437:        "       rating  \\\n",
1438:        "2410        1   \n",
1439:        "2578        5   \n",
1440:        "2605        4   \n",
1441:        "2608        5   \n",
1442:        "2637        5   \n",
1443:        "...       ...   \n",
1444:        "40406       4   \n",
1445:        "40407       5   \n",
1446:        "40408       2   \n",
1447:        "40409       1   \n",
1448:        "40410       5   \n",
1449:        "\n",
1450:        "                                                                                                                                                                                                        review  \\\n",
1451:        "2410   i had a hard time contacting the manufacturer distributor in order to make sure the measurements were correct the description and the pdf have completely different dimensions in reality these didn...   \n",
1452:        "2578   i purchased this bed and have slept on it for the past week i believe in trying things out to make sure my guests won t suffer from backaches etc the aerobed provides a comfortable night s rest i ...   \n",
1453:        "2605   after my first night sleeping on a neckbone pillow i ordered another one so my husband could have his own too i could already feel improvement in my neck and shoulder problems after just one night...   \n",
1454:        "2608   these canisters are the perfect size for us we use the smallest one for powdered creamer the middle size for instant coffee and the largest size for sugar which we use to refill our smaller sugar ...   \n",
1455:        "2637   these are really wonderful they are perfect for strawberry hulling neatly and easily i ve owned a dozen not because they wear out they don t they just seem to wander away when i m not looking fort...   \n",
1456:        "...                                                                                                                                                                                                        ...   \n",
1457:        "40406  i had read some reviews saying that this bra ran small and so i ordered two band and cup sizes up and it was still too small definitely along the lines of a sports bra squish effect the sides do c...   \n",
1458:        "40407  i wasn t sure exactly what it would be it is a little large for my small size but i think it is a nice fit the fabric is a nice thin material but it is a little thin in the legs i wish it was thic...   \n",
1459:        "40408  you can wear the hood by itself wear it with the hood or wear just the jacket without the hood how is that for 3 in 1 systems reminiscent of what lands end sells as a squall jacket or what uniform...   \n",
1460:        "40409  i liked nothing about this dress the only reason i gave it 4 stars is because i ordered the size 6 5 and it fit perfectly the fabric is a nice thin material and the color is vibrant it s a little ...   \n",
1461:        "40410  i work in the wedding industry and have to work long days on my feet outside in the heat and have to look professional i ve spent a ridiculous amount of money on high end dress shoes like merrels ...   \n",
1462:        "\n",
1463:        "       label  \n",
1464:        "2410       0  \n",
1465:        "2578       0  \n",
1466:        "2605       0  \n",
1467:        "2608       0  \n",
1468:        "2637       0  \n",
1469:        "...      ...  \n",
1470:        "40406      0  \n",

(Output capped at 50 KB. Showing lines 1-1470. Use offset=1471 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 3.1s)

_Thinking:_

Let me continue reading the notebook to see the rest of the content.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 1471
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
1471:        "40407      1  \n",
1472:        "40408      0  \n",
1473:        "40409      1  \n",
1474:        "40410      0  \n",
1475:        "\n",
1476:        "[14050 rows x 3 columns]"
1477:       ]
1478:      },
1479:      "execution_count": 257,
1480:      "metadata": {},
1481:      "output_type": "execute_result"
1482:     }
1483:    ],
1484:    "source": [
1485:     "amazon_df[amazon_df[\"review\"].str.len() > 300]"
1486:    ]
1487:   },
1488:   {
1489:    "cell_type": "code",
1490:    "execution_count": 258,
1491:    "id": "395aa86d",
1492:    "metadata": {},
1493:    "outputs": [
1494:     {
1495:      "name": "stdout",
1496:      "output_type": "stream",
1497:      "text": [
1498:       "Empty Reviews : 0\n",
1499:       "Average Review Length : 529.96384\n",
1500:       "Shortest Review Length : 1\n",
1501:       "Longest Review Length : 4907\n"
1502:      ]
1503:     }
1504:    ],
1505:    "source": [
1506:     "#yelp\n",
1507:     "\n",
1508:     "print(\"Empty Reviews :\", (yelp_sample[\"review\"] == \"\").sum())\n",
1509:     "\n",
1510:     "print(\"Average Review Length :\", yelp_sample[\"review\"].str.len().mean())\n",
1511:     "\n",
1512:     "print(\"Shortest Review Length :\", yelp_sample[\"review\"].str.len().min())\n",
1513:     "\n",
1514:     "print(\"Longest Review Length :\", yelp_sample[\"review\"].str.len().max())"
1515:    ]
1516:   },
1517:   {
1518:    "cell_type": "code",
1519:    "execution_count": 259,
1520:    "id": "02f9e6a4",
1521:    "metadata": {},
1522:    "outputs": [
1523:     {
1524:      "data": {
1525:       "text/html": [
1526:        "<div>\n",
1527:        "<style scoped>\n",
1528:        "    .dataframe tbody tr th:only-of-type {\n",
1529:        "        vertical-align: middle;\n",
1530:        "    }\n",
1531:        "\n",
1532:        "    .dataframe tbody tr th {\n",
1533:        "        vertical-align: top;\n",
1534:        "    }\n",
1535:        "\n",
1536:        "    .dataframe thead th {\n",
1537:        "        text-align: right;\n",
1538:        "    }\n",
1539:        "</style>\n",
1540:        "<table border=\"1\" class=\"dataframe\">\n",
1541:        "  <thead>\n",
1542:        "    <tr style=\"text-align: right;\">\n",
1543:        "      <th></th>\n",
1544:        "      <th>rating</th>\n",
1545:        "      <th>review</th>\n",
1546:        "      <th>label</th>\n",
1547:        "    </tr>\n",
1548:        "  </thead>\n",
1549:        "  <tbody>\n",
1550:        "    <tr>\n",
1551:        "      <th>56</th>\n",
1552:        "      <td>5</td>\n",
1553:        "      <td>still the best</td>\n",
1554:        "      <td>1</td>\n",
1555:        "    </tr>\n",
1556:        "    <tr>\n",
1557:        "      <th>75</th>\n",
1558:        "      <td>5</td>\n",
1559:        "      <td>love this place</td>\n",
1560:        "      <td>1</td>\n",
1561:        "    </tr>\n",
1562:        "    <tr>\n",
1563:        "      <th>102</th>\n",
1564:        "      <td>4</td>\n",
1565:        "      <td>good times good drinks great food</td>\n",
1566:        "      <td>1</td>\n",
1567:        "    </tr>\n",
1568:        "    <tr>\n",
1569:        "      <th>149</th>\n",
1570:        "      <td>5</td>\n",
1571:        "      <td>this place is delicious and fun</td>\n",
1572:        "      <td>1</td>\n",
1573:        "    </tr>\n",
1574:        "    <tr>\n",
1575:        "      <th>155</th>\n",
1576:        "      <td>4</td>\n",
1577:        "      <td>do it again very nice place</td>\n",
1578:        "      <td>1</td>\n",
1579:        "    </tr>\n",
1580:        "    <tr>\n",
1581:        "      <th>...</th>\n",
1582:        "      <td>...</td>\n",
1583:        "      <td>...</td>\n",
1584:        "      <td>...</td>\n",
1585:        "    </tr>\n",
1586:        "    <tr>\n",
1587:        "      <th>49862</th>\n",
1588:        "      <td>3</td>\n",
1589:        "      <td>14th and 6th by old navy is way better</td>\n",
1590:        "      <td>1</td>\n",
1591:        "    </tr>\n",
1592:        "    <tr>\n",
1593:        "      <th>49877</th>\n",
1594:        "      <td>5</td>\n",
1595:        "      <td>yum</td>\n",
1596:        "      <td>1</td>\n",
1597:        "    </tr>\n",
1598:        "    <tr>\n",
1599:        "      <th>49883</th>\n",
1600:        "      <td>5</td>\n",
1601:        "      <td>delicious ethiopian all vegan too</td>\n",
1602:        "      <td>0</td>\n",
1603:        "    </tr>\n",
1604:        "    <tr>\n",
1605:        "      <th>49961</th>\n",
1606:        "      <td>4</td>\n",
1607:        "      <td>nom</td>\n",
1608:        "      <td>1</td>\n",
1609:        "    </tr>\n",
1610:        "    <tr>\n",
1611:        "      <th>49996</th>\n",
1612:        "      <td>5</td>\n",
1613:        "      <td>looks good</td>\n",
1614:        "      <td>1</td>\n",
1615:        "    </tr>\n",
1616:        "  </tbody>\n",
1617:        "</table>\n",
1618:        "<p>1665 rows × 3 columns</p>\n",
1619:        "</div>"
1620:       ],
1621:       "text/plain": [
1622:        "       rating                                  review  label\n",
1623:        "56          5                          still the best      1\n",
1624:        "75          5                         love this place      1\n",
1625:        "102         4       good times good drinks great food      1\n",
1626:        "149         5         this place is delicious and fun      1\n",
1627:        "155         4             do it again very nice place      1\n",
1628:        "...       ...                                     ...    ...\n",
1629:        "49862       3  14th and 6th by old navy is way better      1\n",
1630:        "49877       5                                     yum      1\n",
1631:        "49883       5       delicious ethiopian all vegan too      0\n",
1632:        "49961       4                                     nom      1\n",
1633:        "49996       5                              looks good      1\n",
1634:        "\n",
1635:        "[1665 rows x 3 columns]"
1636:       ]
1637:      },
1638:      "execution_count": 259,
1639:      "metadata": {},
1640:      "output_type": "execute_result"
1641:     }
1642:    ],
1643:    "source": [
1644:     "# Print rows where text has fewer than 20 characters\n",
1645:     "yelp_sample[yelp_sample[\"review\"].str.len() < 40]"
1646:    ]
1647:   },
1648:   {
1649:    "cell_type": "code",
1650:    "execution_count": 260,
1651:    "id": "d3a4beb9",
1652:    "metadata": {},
1653:    "outputs": [
1654:     {
1655:      "data": {
1656:       "text/html": [
1657:        "<div>\n",
1658:        "<style scoped>\n",
1659:        "    .dataframe tbody tr th:only-of-type {\n",
1660:        "        vertical-align: middle;\n",
1661:        "    }\n",
1662:        "\n",
1663:        "    .dataframe tbody tr th {\n",
1664:        "        vertical-align: top;\n",
1665:        "    }\n",
1666:        "\n",
1667:        "    .dataframe thead th {\n",
1668:        "        text-align: right;\n",
1669:        "    }\n",
1670:        "</style>\n",
1671:        "<table border=\"1\" class=\"dataframe\">\n",
1672:        "  <thead>\n",
1673:        "    <tr style=\"text-align: right;\">\n",
1674:        "      <th></th>\n",
1675:        "      <th>rating</th>\n",
1676:        "      <th>review</th>\n",
1677:        "      <th>label</th>\n",
1678:        "      <th>review_length</th>\n",
1679:        "    </tr>\n",
1680:        "  </thead>\n",
1681:        "  <tbody>\n",
1682:        "    <tr>\n",
1683:        "      <th>48267</th>\n",
1684:        "      <td>5</td>\n",
1685:        "      <td>cheap and delicious</td>\n",
1686:        "      <td>1</td>\n",
1687:        "      <td>19</td>\n",
1688:        "    </tr>\n",
1689:        "    <tr>\n",
1690:        "      <th>47366</th>\n",
1691:        "      <td>5</td>\n",
1692:        "      <td>very very very good</td>\n",
1693:        "      <td>1</td>\n",
1694:        "      <td>19</td>\n",
1695:        "    </tr>\n",
1696:        "    <tr>\n",
1697:        "      <th>45673</th>\n",
1698:        "      <td>5</td>\n",
1699:        "      <td>great place love it</td>\n",
1700:        "      <td>1</td>\n",
1701:        "      <td>19</td>\n",
1702:        "    </tr>\n",
1703:        "    <tr>\n",
1704:        "      <th>2359</th>\n",
1705:        "      <td>3</td>\n",
1706:        "      <td>white sauce is good</td>\n",
1707:        "      <td>1</td>\n",
1708:        "      <td>19</td>\n",
1709:        "    </tr>\n",
1710:        "    <tr>\n",
1711:        "      <th>3039</th>\n",
1712:        "      <td>4</td>\n",
1713:        "      <td>i loved their tacos</td>\n",
1714:        "      <td>1</td>\n",
1715:        "      <td>19</td>\n",
1716:        "    </tr>\n",
1717:        "    <tr>\n",
1718:        "      <th>...</th>\n",
1719:        "      <td>...</td>\n",
1720:        "      <td>...</td>\n",
1721:        "      <td>...</td>\n",
1722:        "      <td>...</td>\n",
1723:        "    </tr>\n",
1724:        "    <tr>\n",
1725:        "      <th>40750</th>\n",
1726:        "      <td>5</td>\n",
1727:        "      <td>yum</td>\n",
1728:        "      <td>0</td>\n",
1729:        "      <td>3</td>\n",
1730:        "    </tr>\n",
1731:        "    <tr>\n",
1732:        "      <th>49961</th>\n",
1733:        "      <td>4</td>\n",
1734:        "      <td>nom</td>\n",
1735:        "      <td>1</td>\n",
1736:        "      <td>3</td>\n",
1737:        "    </tr>\n",
1738:        "    <tr>\n",
1739:        "      <th>44802</th>\n",
1740:        "      <td>5</td>\n",
1741:        "      <td>woo</td>\n",
1742:        "      <td>1</td>\n",
1743:        "      <td>3</td>\n",
1744:        "    </tr>\n",
1745:        "    <tr>\n",
1746:        "      <th>23950</th>\n",
1747:        "      <td>2</td>\n",
1748:        "      <td>ok</td>\n",
1749:        "      <td>1</td>\n",
1750:        "      <td>2</td>\n",
1751:        "    </tr>\n",
1752:        "    <tr>\n",
1753:        "      <th>421</th>\n",
1754:        "      <td>5</td>\n",
1755:        "      <td>5</td>\n",
1756:        "      <td>1</td>\n",
1757:        "      <td>1</td>\n",
1758:        "    </tr>\n",
1759:        "  </tbody>\n",
1760:        "</table>\n",
1761:        "<p>570 rows × 4 columns</p>\n",
1762:        "</div>"
1763:       ],
1764:       "text/plain": [
1765:        "       rating               review  label  review_length\n",
1766:        "48267       5  cheap and delicious      1             19\n",
1767:        "47366       5  very very very good      1             19\n",
1768:        "45673       5  great place love it      1             19\n",
1769:        "2359        3  white sauce is good      1             19\n",
1770:        "3039        4  i loved their tacos      1             19\n",
1771:        "...       ...                  ...    ...            ...\n",
1772:        "40750       5                  yum      0              3\n",
1773:        "49961       4                  nom      1              3\n",
1774:        "44802       5                  woo      1              3\n",
1775:        "23950       2                   ok      1              2\n",
1776:        "421         5                    5      1              1\n",
1777:        "\n",
1778:        "[570 rows x 4 columns]"
1779:       ]
1780:      },
1781:      "execution_count": 260,
1782:      "metadata": {},
1783:      "output_type": "execute_result"
1784:     }
1785:    ],
1786:    "source": [
1787:     "yelp_sample[\n",
1788:     "    yelp_sample[\"review\"].str.len() < 20\n",
1789:     "].assign(\n",
1790:     "    review_length=yelp_sample[\"review\"].str.len()\n",
1791:     ").sort_values(\n",
1792:     "    by=\"review_length\", ascending=False\n",
1793:     ")"
1794:    ]
1795:   },
1796:   {
1797:    "cell_type": "code",
1798:    "execution_count": 261,
1799:    "id": "f96d07a5",
1800:    "metadata": {},
1801:    "outputs": [
1802:     {
1803:      "data": {
1804:       "text/html": [
1805:        "<div>\n",
1806:        "<style scoped>\n",
1807:        "    .dataframe tbody tr th:only-of-type {\n",
1808:        "        vertical-align: middle;\n",
1809:        "    }\n",
1810:        "\n",
1811:        "    .dataframe tbody tr th {\n",
1812:        "        vertical-align: top;\n",
1813:        "    }\n",
1814:        "\n",
1815:        "    .dataframe thead th {\n",
1816:        "        text-align: right;\n",
1817:        "    }\n",
1818:        "</style>\n",
1819:        "<table border=\"1\" class=\"dataframe\">\n",
1820:        "  <thead>\n",
1821:        "    <tr style=\"text-align: right;\">\n",
1822:        "      <th></th>\n",
1823:        "      <th>rating</th>\n",
1824:        "      <th>review</th>\n",
1825:        "      <th>label</th>\n",
1826:        "    </tr>\n",
1827:        "  </thead>\n",
1828:        "  <tbody>\n",
1829:        "    <tr>\n",
1830:        "      <th>1</th>\n",
1831:        "      <td>2</td>\n",
1832:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
1833:        "      <td>0</td>\n",
1834:        "    </tr>\n",
1835:        "    <tr>\n",
1836:        "      <th>2</th>\n",
1837:        "      <td>3</td>\n",
1838:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
1839:        "      <td>0</td>\n",
1840:        "    </tr>\n",
1841:        "    <tr>\n",
1842:        "      <th>3</th>\n",
1843:        "      <td>2</td>\n",
1844:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
1845:        "      <td>0</td>\n",
1846:        "    </tr>\n",
1847:        "    <tr>\n",
1848:        "      <th>5</th>\n",
1849:        "      <td>1</td>\n",
1850:        "      <td>i went to this restaurant last saturday based on the reviews that my friend saw on yelp well i can easily say that this is the worst food i have ever eaten at a restaurant i have no idea what thos...</td>\n",
1851:        "      <td>1</td>\n",
1852:        "    </tr>\n",
1853:        "    <tr>\n",
1854:        "      <th>6</th>\n",
1855:        "      <td>4</td>\n",
1856:        "      <td>place was nice looking staff were friendly and food was delicious we were seated in the main dining area as there were no seats available in the back yard a c was pumping and place was a bit chill...</td>\n",
1857:        "      <td>0</td>\n",
1858:        "    </tr>\n",
1859:        "    <tr>\n",
1860:        "      <th>...</th>\n",
1861:        "      <td>...</td>\n",
1862:        "      <td>...</td>\n",
1863:        "      <td>...</td>\n",
1864:        "    </tr>\n",
1865:        "    <tr>\n",
1866:        "      <th>49988</th>\n",
1867:        "      <td>3</td>\n",
1868:        "      <td>good very inexpensive basic cantonese food you can even eat healthy here if you are careful about what you order more of a lunch place than dinner if you care about cleanliness you will mind the s...</td>\n",
1869:        "      <td>0</td>\n",
1870:        "    </tr>\n",
1871:        "    <tr>\n",
1872:        "      <th>49989</th>\n",
1873:        "      <td>2</td>\n",
1874:        "      <td>david chang you may be slightly overrated went with a group of six we ordered 1 the kimchee w pears 2 hamachi 3 oysters w kimchee foam 4 the pork buns and of course 5 the pork shoulder the best by...</td>\n",
1875:        "      <td>1</td>\n",
1876:        "    </tr>\n",
1877:        "    <tr>\n",
1878:        "      <th>49990</th>\n",
1879:        "      <td>5</td>\n",
1880:        "      <td>first went to soco a few weeks before the grand opening the grand opening was in late july so im guessing late june is when i first went they were only open sporadically then and they were testing...</td>\n",
1881:        "      <td>1</td>\n",
1882:        "    </tr>\n",
1883:        "    <tr>\n",
1884:        "      <th>49992</th>\n",
1885:        "      <td>5</td>\n",
1886:        "      <td>a friend was in town and i learned this was her spot the must do thing on the line up having never been sounded good to me everything was under complete control here you walked in and you either h...</td>\n",
1887:        "      <td>1</td>\n",
1888:        "    </tr>\n",
1889:        "    <tr>\n",
1890:        "      <th>49998</th>\n",
1891:        "      <td>5</td>\n",
1892:        "      <td>laissez les bons temps rouler who on earth would ever guess that this place would be on satan s island if it weren t for the b f living here i wouldn t visit or pay the toll but for bayou i would ...</td>\n",
1893:        "      <td>0</td>\n",
1894:        "    </tr>\n",
1895:        "  </tbody>\n",
1896:        "</table>\n",
1897:        "<p>18962 rows × 3 columns</p>\n",
1898:        "</div>"
1899:       ],
1900:       "text/plain": [
1901:        "       rating  \\\n",
1902:        "1           2   \n",
1903:        "2           3   \n",
1904:        "3           2   \n",
1905:        "5           1   \n",
1906:        "6           4   \n",
1907:        "...       ...   \n",
1908:        "49988       3   \n",
1909:        "49989       2   \n",
1910:        "49990       5   \n",
1911:        "49992       5   \n",
1912:        "49998       5   \n",
1913:        "\n",
1914:        "                                                                                                                                                                                                        review  \\\n",
1915:        "1      the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
1916:        "2      very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
1917:        "3      i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
1918:        "5      i went to this restaurant last saturday based on the reviews that my friend saw on yelp well i can easily say that this is the worst food i have ever eaten at a restaurant i have no idea what thos...   \n",
1919:        "6      place was nice looking staff were friendly and food was delicious we were seated in the main dining area as there were no seats available in the back yard a c was pumping and place was a bit chill...   \n",
1920:        "...                                                                                                                                                                                                        ...   \n",
1921:        "49988  good very inexpensive basic cantonese food you can even eat healthy here if you are careful about what you order more of a lunch place than dinner if you care about cleanliness you will mind the s...   \n",
1922:        "49989  david chang you may be slightly overrated went with a group of six we ordered 1 the kimchee w pears 2 hamachi 3 oysters w kimchee foam 4 the pork buns and of course 5 the pork shoulder the best by...   \n",
1923:        "49990  first went to soco a few weeks before the grand opening the grand opening was in late july so im guessing late june is when i first went they were only open sporadically then and they were testing...   \n",
1924:        "49992  a friend was in town and i learned this was her spot the must do thing on the line up having never been sounded good to me everything was under complete control here you walked in and you either h...   \n",
1925:        "49998  laissez les bons temps rouler who on earth would ever guess that this place would be on satan s island if it weren t for the b f living here i wouldn t visit or pay the toll but for bayou i would ...   \n",
1926:        "\n",
1927:        "       label  \n",
1928:        "1          0  \n",
1929:        "2          0  \n",
1930:        "3          0  \n",
1931:        "5          1  \n",
1932:        "6          0  \n",
1933:        "...      ...  \n",
1934:        "49988      0  \n",
1935:        "49989      1  \n",
1936:        "49990      1  \n",
1937:        "49992      1  \n",
1938:        "49998      0  \n",
1939:        "\n",
1940:        "[18962 rows x 3 columns]"
1941:       ]
1942:      },
1943:      "execution_count": 261,
1944:      "metadata": {},
1945:      "output_type": "execute_result"
1946:     }
1947:    ],
1948:    "source": [
1949:     "yelp_sample[yelp_sample[\"review\"].str.len() > 500]"
1950:    ]
1951:   },
1952:   {
1953:    "cell_type": "code",
1954:    "execution_count": 262,
1955:    "id": "f1b0f41e",
1956:    "metadata": {},
1957:    "outputs": [],
1958:    "source": [
1959:     "yelp_sample = yelp_sample[yelp_sample[\"review\"].str.len() >= 20]"
1960:    ]
1961:   },
1962:   {
1963:    "cell_type": "code",
1964:    "execution_count": 263,
1965:    "id": "49439f21",
1966:    "metadata": {},
1967:    "outputs": [],
1968:    "source": [
1969:     "amazon_df=amazon_df[amazon_df[\"review\"].str.len() >= 20]"
1970:    ]
1971:   },
1972:   {
1973:    "cell_type": "code",
1974:    "execution_count": 264,
1975:    "id": "e54669f8",
1976:    "metadata": {},
1977:    "outputs": [
1978:     {
1979:      "name": "stdout",
1980:      "output_type": "stream",
1981:      "text": [
1982:       "Empty Reviews : 0\n",
1983:       "Average Review Length : 535.9302043293546\n",
1984:       "Shortest Review Length : 20\n",
1985:       "Longest Review Length : 4907\n"
1986:      ]
1987:     }
1988:    ],
1989:    "source": [
1990:     "#yelp\n",
1991:     "\n",
1992:     "print(\"Empty Reviews :\", (yelp_sample[\"review\"] == \"\").sum())\n",
1993:     "\n",
1994:     "print(\"Average Review Length :\", yelp_sample[\"review\"].str.len().mean())\n",
1995:     "\n",
1996:     "print(\"Shortest Review Length :\", yelp_sample[\"review\"].str.len().min())\n",
1997:     "\n",
1998:     "print(\"Longest Review Length :\", yelp_sample[\"review\"].str.len().max())"
1999:    ]
2000:   },
2001:   {
2002:    "cell_type": "code",
2003:    "execution_count": 265,
2004:    "id": "a1ac3c21",
2005:    "metadata": {},
2006:    "outputs": [
2007:     {
2008:      "name": "stdout",
2009:      "output_type": "stream",
2010:      "text": [
2011:       "Empty Reviews : 0\n",
2012:       "Average Review Length : 339.9354319796075\n",
2013:       "Shortest Review Length : 24\n",
2014:       "Longest Review Length : 2095\n"
2015:      ]
2016:     }
2017:    ],
2018:    "source": [
2019:     "#amazon\n",
2020:     "\n",
2021:     "print(\"Empty Reviews :\", (amazon_df[\"review\"] == \"\").sum())\n",
2022:     "\n",
2023:     "print(\"Average Review Length :\", amazon_df[\"review\"].str.len().mean())\n",
2024:     "\n",
2025:     "print(\"Shortest Review Length :\", amazon_df[\"review\"].str.len().min())\n",
2026:     "\n",
2027:     "print(\"Longest Review Length :\", amazon_df[\"review\"].str.len().max())"
2028:    ]
2029:   },
2030:   {
2031:    "cell_type": "markdown",
2032:    "id": "afeac13d",
2033:    "metadata": {},
2034:    "source": [
2035:     "### EDA"
2036:    ]
2037:   },
2038:   {
2039:    "cell_type": "code",
2040:    "execution_count": 266,
2041:    "id": "fa86f547",
2042:    "metadata": {},
2043:    "outputs": [
2044:     {
2045:      "name": "stderr",
2046:      "output_type": "stream",
2047:      "text": [
2048:       "/opt/python-venvs/work/lib/python3.12/site-packages/nltk/downloader.py:1076: UserWarning: NLTK will not authorize the non-private download directory '/home/hitesh/nltk_data': it (or an ancestor) is world- or group-writable, so another local user could plant files there. Choose a private location such as ~/nltk_data.\n",
2049:       "  for msg in self.incr_download(info_or_id, download_dir, force):\n",
2050:       "[nltk_data] Downloading package punkt to /home/hitesh/nltk_data...\n",
2051:       "[nltk_data]   Package punkt is already up-to-date!\n",
2052:       "[nltk_data] Downloading package punkt_tab to /home/hitesh/nltk_data...\n",
2053:       "[nltk_data]   Package punkt_tab is already up-to-date!\n"
2054:      ]
2055:     },
2056:     {
2057:      "data": {
2058:       "text/plain": [
2059:        "True"
2060:       ]
2061:      },
2062:      "execution_count": 266,
2063:      "metadata": {},
2064:      "output_type": "execute_result"
2065:     }
2066:    ],
2067:    "source": [
2068:     "import matplotlib.pyplot as plt\n",
2069:     "from wordcloud import WordCloud\n",
2070:     "from collections import Counter\n",
2071:     "from sklearn.feature_extraction.text import CountVectorizer\n",
2072:     "import nltk\n",
2073:     "\n",
2074:     "nltk.download(\"punkt\")\n",
2075:     "nltk.download(\"punkt_tab\")"
2076:    ]
2077:   },
2078:   {
2079:    "cell_type": "code",
2080:    "execution_count": null,
2081:    "id": "5ee472a0",
2082:    "metadata": {},
2083:    "outputs": [],
2084:    "source": []
2085:   },
2086:   {
2087:    "cell_type": "code",
2088:    "execution_count": 267,
2089:    "id": "3a88a628",
2090:    "metadata": {},
2091:    "outputs": [
2092:     {
2093:      "name": "stdout",
2094:      "output_type": "stream",
2095:      "text": [
2096:       "Dataset Shape : (40407, 3)\n",
2097:       "\n",
2098:       "Class Distribution:\n",
2099:       "\n",
2100:       "label\n",
2101:       "0    20215\n",
2102:       "1    20192\n",
2103:       "Name: count, dtype: int64\n"
2104:      ]
2105:     },
2106:     {
2107:      "data": {
2108:       "text/html": [
2109:        "<div>\n",
2110:        "<style scoped>\n",
2111:        "    .dataframe tbody tr th:only-of-type {\n",
2112:        "        vertical-align: middle;\n",
2113:        "    }\n",
2114:        "\n",
2115:        "    .dataframe tbody tr th {\n",
2116:        "        vertical-align: top;\n",
2117:        "    }\n",
2118:        "\n",
2119:        "    .dataframe thead th {\n",
2120:        "        text-align: right;\n",
2121:        "    }\n",
2122:        "</style>\n",
2123:        "<table border=\"1\" class=\"dataframe\">\n",
2124:        "  <thead>\n",
2125:        "    <tr style=\"text-align: right;\">\n",
2126:        "      <th></th>\n",
2127:        "      <th>rating</th>\n",
2128:        "      <th>review</th>\n",
2129:        "      <th>label</th>\n",
2130:        "    </tr>\n",
2131:        "  </thead>\n",
2132:        "  <tbody>\n",
2133:        "    <tr>\n",
2134:        "      <th>0</th>\n",
2135:        "      <td>5</td>\n",
2136:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2137:        "      <td>1</td>\n",
2138:        "    </tr>\n",
2139:        "    <tr>\n",
2140:        "      <th>1</th>\n",
2141:        "      <td>5</td>\n",
2142:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2143:        "      <td>1</td>\n",
2144:        "    </tr>\n",
2145:        "    <tr>\n",
2146:        "      <th>2</th>\n",
2147:        "      <td>5</td>\n",
2148:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2149:        "      <td>1</td>\n",
2150:        "    </tr>\n",
2151:        "    <tr>\n",
2152:        "      <th>3</th>\n",
2153:        "      <td>1</td>\n",
2154:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2155:        "      <td>1</td>\n",
2156:        "    </tr>\n",
2157:        "    <tr>\n",
2158:        "      <th>4</th>\n",
2159:        "      <td>5</td>\n",
2160:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2161:        "      <td>1</td>\n",
2162:        "    </tr>\n",
2163:        "  </tbody>\n",
2164:        "</table>\n",
2165:        "</div>"
2166:       ],
2167:       "text/plain": [
2168:        "   rating  \\\n",
2169:        "0       5   \n",
2170:        "1       5   \n",
2171:        "2       5   \n",
2172:        "3       1   \n",
2173:        "4       5   \n",
2174:        "\n",
2175:        "                                                                                review  \\\n",
2176:        "0                love this well made sturdy and very comfortable i love it very pretty   \n",
2177:        "1        love it a great upgrade from the original i ve had mine for a couple of years   \n",
2178:        "2                    this pillow saved my back i love the look and feel of this pillow   \n",
2179:        "3       missing information on how to use it but it is a great product for the price i   \n",
2180:        "4  very nice set good quality we have had the set for two months now and have not been   \n",
2181:        "\n",
2182:        "   label  \n",
2183:        "0      1  \n",
2184:        "1      1  \n",
2185:        "2      1  \n",
2186:        "3      1  \n",
2187:        "4      1  "
2188:       ]
2189:      },
2190:      "execution_count": 267,
2191:      "metadata": {},
2192:      "output_type": "execute_result"
2193:     }
2194:    ],
2195:    "source": [
2196:     "#amazon\n",
2197:     "\n",
2198:     "print(\"Dataset Shape :\", amazon_df.shape)\n",
2199:     "print(\"\\nClass Distribution:\\n\")\n",
2200:     "print(amazon_df[\"label\"].value_counts())\n",
2201:     "\n",
2202:     "amazon_df.head()"
2203:    ]
2204:   },
2205:   {
2206:    "cell_type": "code",
2207:    "execution_count": 268,
2208:    "id": "b98ee1c0",
2209:    "metadata": {},
2210:    "outputs": [
2211:     {
2212:      "name": "stdout",
2213:      "output_type": "stream",
2214:      "text": [
2215:       "Dataset Shape : (49430, 3)\n",
2216:       "\n",
2217:       "Class Distribution:\n",
2218:       "\n",
2219:       "label\n",
2220:       "0    24883\n",
2221:       "1    24547\n",
2222:       "Name: count, dtype: int64\n"
2223:      ]
2224:     },
2225:     {
2226:      "data": {
2227:       "text/html": [
2228:        "<div>\n",
2229:        "<style scoped>\n",
2230:        "    .dataframe tbody tr th:only-of-type {\n",
2231:        "        vertical-align: middle;\n",
2232:        "    }\n",
2233:        "\n",
2234:        "    .dataframe tbody tr th {\n",
2235:        "        vertical-align: top;\n",
2236:        "    }\n",
2237:        "\n",
2238:        "    .dataframe thead th {\n",
2239:        "        text-align: right;\n",
2240:        "    }\n",
2241:        "</style>\n",
2242:        "<table border=\"1\" class=\"dataframe\">\n",
2243:        "  <thead>\n",
2244:        "    <tr style=\"text-align: right;\">\n",
2245:        "      <th></th>\n",
2246:        "      <th>rating</th>\n",
2247:        "      <th>review</th>\n",
2248:        "      <th>label</th>\n",
2249:        "    </tr>\n",
2250:        "  </thead>\n",
2251:        "  <tbody>\n",
2252:        "    <tr>\n",
2253:        "      <th>0</th>\n",
2254:        "      <td>5</td>\n",
2255:        "      <td>my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...</td>\n",
2256:        "      <td>1</td>\n",
2257:        "    </tr>\n",
2258:        "    <tr>\n",
2259:        "      <th>1</th>\n",
2260:        "      <td>2</td>\n",
2261:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2262:        "      <td>0</td>\n",
2263:        "    </tr>\n",
2264:        "    <tr>\n",
2265:        "      <th>2</th>\n",
2266:        "      <td>3</td>\n",
2267:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2268:        "      <td>0</td>\n",
2269:        "    </tr>\n",
2270:        "    <tr>\n",
2271:        "      <th>3</th>\n",
2272:        "      <td>2</td>\n",
2273:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2274:        "      <td>0</td>\n",
2275:        "    </tr>\n",
2276:        "    <tr>\n",
2277:        "      <th>4</th>\n",
2278:        "      <td>5</td>\n",
2279:        "      <td>my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried</td>\n",
2280:        "      <td>1</td>\n",
2281:        "    </tr>\n",
2282:        "  </tbody>\n",
2283:        "</table>\n",
2284:        "</div>"
2285:       ],
2286:       "text/plain": [
2287:        "   rating  \\\n",
2288:        "0       5   \n",
2289:        "1       2   \n",
2290:        "2       3   \n",
2291:        "3       2   \n",
2292:        "4       5   \n",
2293:        "\n",
2294:        "                                                                                                                                                                                                    review  \\\n",
2295:        "0  my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...   \n",
2296:        "1  the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2297:        "2  very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2298:        "3  i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2299:        "4                                                my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried   \n",
2300:        "\n",
2301:        "   label  \n",
2302:        "0      1  \n",
2303:        "1      0  \n",
2304:        "2      0  \n",
2305:        "3      0  \n",
2306:        "4      1  "
2307:       ]
2308:      },
2309:      "execution_count": 268,
2310:      "metadata": {},
2311:      "output_type": "execute_result"
2312:     }
2313:    ],
2314:    "source": [
2315:     "#Yelp\n",
2316:     "\n",
2317:     "print(\"Dataset Shape :\", yelp_sample.shape)\n",
2318:     "print(\"\\nClass Distribution:\\n\")\n",
2319:     "print(yelp_sample[\"label\"].value_counts())\n",
2320:     "\n",
2321:     "yelp_sample.head()"
2322:    ]
2323:   },
2324:   {
2325:    "cell_type": "code",
2326:    "execution_count": 269,
2327:    "id": "c94a51a5",
2328:    "metadata": {},
2329:    "outputs": [
2330:     {
2331:      "data": {
2332:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAi8AAAF1CAYAAAAgKQpIAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAV/9JREFUeJzt3XdYFFfbBvAbEVYUaRZsCCh2sWBFRFHAig27YgWNUZPYEjXGmtiS12g0ftEIGntiT9TYUEFRMRjFqFjABjakCKuCSDnfH77M67gL7q6LsOb+Xddel3vmmTPP7jq7D2fOzBgJIQSIiIiIDESxwk6AiIiISBssXoiIiMigsHghIiIig8LihYiIiAwKixciIiIyKCxeiIiIyKCweCEiIiKDwuKFiIiIDAqLl3+ZxMREBAYG4u7du4W2vQcPHiAwMBAPHjx4LznklUdR9fDhQ+zZswdBQUE4f/58YaejN4b0GdCHLTIyEoGBgcjKyirsVPJ069YtBAYG4smTJ4WdSpFUvLATIN0plUps27ZNel68eHFYWFjA3t4e9evXh0KhUFnnzp07GDVqFHbv3g17e3uNtxUfH4+9e/eiY8eOsLOz03g9dduLiorCqFGjcOTIEVSqVEnjvt4lR11f9/t28OBB9O7dG61bt4adnR3KlSsHFxeXfNcRQuDy5cu4ceMG0tPTUbFiRTg6OqJatWrvKWvNGMpn8K6ys7Pxyy+/AACGDx8OY2NjlZjcfbdhw4Zo1qyZVv0/f/4cf/31Fx48eACFQoEqVaqgTp06sLS01Ef6RcaJEydw7949DBo0SO9979u3DzNnzsSAAQNgbm6eZ1xERAQuXrwoPTcxMUGFChXg6uoKCwsLvef1ur/++gujRo1Cy5YtYW1tXaDbMkQsXgzY48ePMWrUKDRo0ADNmjWDEAIpKSm4dOkSHj58iEGDBmH+/PkoW7astE65cuXg7+8PBwcHrbYVHR2NUaNGYe/evVoVL7puTxf55fg+83gXc+bMgZubGw4dOqRR/LZt2zB9+nQolUq4urrCysoK9+7dQ1hYGOrWrYuZM2eid+/eBZy1ZgzlM3hX+/fvR0BAAACgfPny6Natm0pM7r47depUjYuX58+fY9q0aQgMDESNGjVQr149CCEQGRmJO3fuoFu3bli2bBkqV66s19dTWNauXYuDBw8WSPGiqZ07d2Lx4sXo27cvLCwskJaWhjNnziAhIQErVqzAiBEjCmzb1atXh7+/P2xsbApsGwZNkMGKjo4WAMTUqVNVlh0/flxUrlxZ2NvbiwcPHrzztk6ePCkAiL17975zX0eOHBEAxJEjR965r9fpM8fCYm1tLcaMGaNR7LfffisAiNmzZ4uMjAzZskePHonBgweLwYMHF0SalI9u3bqJevXqiXr16onu3burjclv31Xn2bNnwsXFRVSsWFGcPHlSZXlwcLCoXr26OH78+LukXqQMGzZM2NraFkjfX3/9tQAgnj59mm/c1KlTBQARHR0ttb148UK0bt1aGBsbi5iYmALJj96OIy8fKA8PD+zatQstWrTA559/jk2bNgF4Ne9gz5498Pb2lg3dZ2Vl4fTp07h37550qKJMmTIAgJs3b2Lfvn0AgMOHD+PRo0cAgBYtWsDZ2RkPHjzAn3/+iS5dusDW1hahoaG4e/cuevbsiezsbLXbe327R48eRWJiIlxcXFCnTh3Z8ujoaISGhqJv376yYfG0tDRs2bIFrVq1Qt26dd+aY16vGwBSUlIQFhaGJ0+eoEqVKnBzc4Opqam0/PXXV6FCBRw/fhwPHz5Eo0aNUL9+fY0/k/y2ExUVhdOnT+Pp06e4fv06AgMDAQCDBw+GmZmZSl9Xr17FtGnTMGzYMMyZM0dlua2tLTZt2oRz586pLMvIyJA+aysrK7Rt21Y2BK7N69X08wHU/9/T5b19W/5vyj2c2KZNG9SsWVNl+YYNG2BnZ4d27doByH9feJvc... (line truncated to 2000 chars)
2333:       "text/plain": [
2334:        "<Figure size 600x400 with 1 Axes>"
2335:       ]
2336:      },
2337:      "metadata": {},
2338:      "output_type": "display_data"
2339:     }
2340:    ],
2341:    "source": [
2342:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
2343:     "\n",
2344:     "plt.figure(figsize=(6,4))\n",
2345:     "plt.bar([\"Genuine (0)\", \"AI Generated (1)\"], label_counts.values)\n",
2346:     "plt.title(\"Distribution of Genuine vs AI-Generated Reviews\")\n",
2347:     "plt.ylabel(\"Number of Reviews\")\n",
2348:     "\n",
2349:     "for i, value in enumerate(label_counts.values):\n",
2350:     "    plt.text(i, value, str(value), ha=\"center\", va=\"bottom\")\n",
2351:     "\n",
2352:     "plt.show()"
2353:    ]
2354:   },
2355:   {
2356:    "cell_type": "code",
2357:    "execution_count": 270,
2358:    "id": "c8e7b73f",
2359:    "metadata": {},
2360:    "outputs": [
2361:     {
2362:      "data": {
2363:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAi8AAAF1CAYAAAAgKQpIAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAT2hJREFUeJzt3XdYFFfbBvAbaaIIWBAbAgIWFAt2EQUpdmMQRYMd7CYxGqMm9hhbijHq92oESyxJ7EaNYkOxEgxiw4INsCFFQKUocL4/fJnXcRdYlkXY5P5d116Xe+aZM8/sOrsPZ87M6gghBIiIiIi0RLnSToCIiIioKFi8EBERkVZh8UJERERahcULERERaRUWL0RERKRVWLwQERGRVmHxQkRERFqFxQsRERFpFRYv/zKJiYkIDAxETExMqW3v0aNHCAwMxKNHj95LDvnlUVY9fvwYe/bsQVBQECIiIko7HY3RpveA/tkiIyMRGBiI7Ozs0k4lX3fv3kVgYCCePXtW2qmUSXqlnQCpLy0tDdu2bZOe6+npwcTEBFZWVmjSpAkMDQ0V1rl//z5GjRqF3bt3w8rKSuVtxcfHY9++fejatSssLS1VXk/Z9qKiojBq1CgcOXIEtWrVUrmv4uSo7n6/b4cOHUK/fv3QsWNHWFpawtzcHE5OTgWuI4TA1atXcevWLWRkZKBmzZqwsbFBvXr13lPWqtGW96C4cnJysGHDBgDA8OHDoaurqxCTd+w2a9YMrVu3LlL/L1++xF9//YVHjx7B0NAQderUQaNGjWBqaqqJ9MuM0NBQPHjwAB999JHG+96/fz9mzZqFgQMHwtjYON+48PBwXLp0SXqur6+PGjVqoH379jAxMdF4Xm/766+/MGrUKLRr1w6VK1cu0W1pIxYvWuzp06cYNWoUmjZtitatW0MIgZSUFFy5cgWPHz/GRx99hG+++QbVqlWT1jE3N4e/vz+sra2LtK3o6GiMGjUK+/btK1Lxou721FFQju8zj+KYO3cunJ2dERwcrFL8tm3bMGPGDKSlpaF9+/YwMzPDgwcPcPr0aTg4OGDWrFno169fCWetGm15D4rrwIEDCAgIAABUr14dvXv3VojJO3anTZumcvHy8uVLTJ8+HYGBgbC3t0fjxo0hhEBkZCTu37+P3r1748cff0Tt2rU1uj+lZd26dTh06FCJFC+q2rlzJ5YsWYL+/fvDxMQE6enpOHfuHBISErBixQqMGDGixLZta2sLf39/VKlSpcS2odUEaa3o6GgBQEybNk1hWUhIiKhdu7awsrISjx49Kva2Tp06JQCIffv2FbuvI0eOCADiyJEjxe7rbZrMsbRUrlxZjB07VqXYpUuXCgBizpw5IisrS7bsyZMnws/PT/j5+ZVEmlSA3r17i8aNG4vGjRuLPn36KI0p6NhV5sWLF8LJyUnUrFlTnDp1SmH50aNHha2trQgJCSlO6mXKsGHDhIWFRYn0/fXXXwsA4vnz5wXGTZs2TQAQ0dHRUltmZqbo2LGj0NXVFbdv3y6R/KhwHHn5h3J1dcWuXbvQtm1bTJ06FZs3bwbwZt7Bnj174OnpKRu6z87OxtmzZ/HgwQPpVEXVqlUBAHfu3MH+/fsBAIcPH8aTJ08AAG3btoWjoyMePXqEP//8Ez169ICFhQVOnjyJmJgY9O3bFzk5OUq39/Z2jx07hsTERDg5OaFRo0ay5dHR0Th58iT69+8vGxZPT0/H1q1b0aFDBzg4OBSaY377DQApKSk4ffo0nj17hjp16sDZ2RkGBgbS8rf3r0aNGggJCcHjx4/RvHlzNGnSROX3pKDtREVF4ezZs3j+/Dlu3ryJwMBAAICfnx+MjIwU+rp+/TqmT5+OYcOGYe7cuQrLLSwssHnzZly4cEFhWVZWlvRem5mZoXPnzrIh8KLsr6rvD6D8/546r21h+b8r73Rip06dUL9+fYXlv/zyCywtLeHm5gag4GOhMHn7s3z5... (line truncated to 2000 chars)
2364:       "text/plain": [
2365:        "<Figure size 600x400 with 1 Axes>"
2366:       ]
2367:      },
2368:      "metadata": {},
2369:      "output_type": "display_data"
2370:     }
2371:    ],
2372:    "source": [
2373:     "label_counts = yelp_sample[\"label\"].value_counts().sort_index()\n",
2374:     "\n",
2375:     "plt.figure(figsize=(6,4))\n",
2376:     "plt.bar([\"Genuine (0)\", \"AI Generated (1)\"], label_counts.values)\n",
2377:     "plt.title(\"Distribution of Genuine vs AI-Generated Reviews\")\n",
2378:     "plt.ylabel(\"Number of Reviews\")\n",
2379:     "\n",
2380:     "for i, value in enumerate(label_counts.values):\n",
2381:     "    plt.text(i, value, str(value), ha=\"center\", va=\"bottom\")\n",
2382:     "\n",
2383:     "plt.show()"
2384:    ]
2385:   },
2386:   {
2387:    "cell_type": "code",
2388:    "execution_count": 271,
2389:    "id": "37794fd1",
2390:    "metadata": {},
2391:    "outputs": [
2392:     {
2393:      "data": {
2394:       "text/html": [
2395:        "<div>\n",
2396:        "<style scoped>\n",
2397:        "    .dataframe tbody tr th:only-of-type {\n",
2398:        "        vertical-align: middle;\n",
2399:        "    }\n",
2400:        "\n",
2401:        "    .dataframe tbody tr th {\n",
2402:        "        vertical-align: top;\n",
2403:        "    }\n",
2404:        "\n",
2405:        "    .dataframe thead th {\n",
2406:        "        text-align: right;\n",
2407:        "    }\n",
2408:        "</style>\n",
2409:        "<table border=\"1\" class=\"dataframe\">\n",
2410:        "  <thead>\n",
2411:        "    <tr style=\"text-align: right;\">\n",
2412:        "      <th></th>\n",
2413:        "      <th>review</th>\n",
2414:        "      <th>text_length</th>\n",
2415:        "      <th>word_count</th>\n",
2416:        "      <th>sentence_count</th>\n",
2417:        "    </tr>\n",
2418:        "  </thead>\n",
2419:        "  <tbody>\n",
2420:        "    <tr>\n",
2421:        "      <th>0</th>\n",
2422:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2423:        "      <td>69</td>\n",
2424:        "      <td>13</td>\n",
2425:        "      <td>1</td>\n",
2426:        "    </tr>\n",
2427:        "    <tr>\n",
2428:        "      <th>1</th>\n",
2429:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2430:        "      <td>77</td>\n",
2431:        "      <td>17</td>\n",
2432:        "      <td>1</td>\n",
2433:        "    </tr>\n",
2434:        "    <tr>\n",
2435:        "      <th>2</th>\n",
2436:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2437:        "      <td>65</td>\n",
2438:        "      <td>14</td>\n",
2439:        "      <td>1</td>\n",
2440:        "    </tr>\n",
2441:        "    <tr>\n",
2442:        "      <th>3</th>\n",
2443:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2444:        "      <td>78</td>\n",
2445:        "      <td>17</td>\n",
2446:        "      <td>1</td>\n",
2447:        "    </tr>\n",
2448:        "    <tr>\n",
2449:        "      <th>4</th>\n",
2450:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2451:        "      <td>83</td>\n",
2452:        "      <td>18</td>\n",
2453:        "      <td>1</td>\n",
2454:        "    </tr>\n",
2455:        "  </tbody>\n",
2456:        "</table>\n",
2457:        "</div>"
2458:       ],
2459:       "text/plain": [
2460:        "                                                                                review  \\\n",
2461:        "0                love this well made sturdy and very comfortable i love it very pretty   \n",
2462:        "1        love it a great upgrade from the original i ve had mine for a couple of years   \n",
2463:        "2                    this pillow saved my back i love the look and feel of this pillow   \n",
2464:        "3       missing information on how to use it but it is a great product for the price i   \n",
2465:        "4  very nice set good quality we have had the set for two months now and have not been   \n",
2466:        "\n",
2467:        "   text_length  word_count  sentence_count  \n",
2468:        "0           69          13               1  \n",
2469:        "1           77          17               1  \n",
2470:        "2           65          14               1  \n",
2471:        "3           78          17               1  \n",
2472:        "4           83          18               1  "
2473:       ]
2474:      },
2475:      "execution_count": 271,
2476:      "metadata": {},
2477:      "output_type": "execute_result"
2478:     }
2479:    ],
2480:    "source": [
2481:     "#feature engineering for amazon\n",
2482:     "\n",
2483:     "amazon_df[\"text_length\"] = amazon_df[\"review\"].str.len()\n",
2484:     "\n",
2485:     "amazon_df[\"word_count\"] = amazon_df[\"review\"].str.split().apply(len)\n",
2486:     "\n",
2487:     "amazon_df[\"sentence_count\"] = amazon_df[\"review\"].apply(\n",
2488:     "    lambda x: len([s for s in nltk.sent_tokenize(x) if s.strip()])\n",
2489:     ")\n",
2490:     "\n",
2491:     "amazon_df[[\"review\",\"text_length\", \"word_count\", \"sentence_count\"]].head()"
2492:    ]
2493:   },
2494:   {
2495:    "cell_type": "code",
2496:    "execution_count": 272,
2497:    "id": "6080e6ea",
2498:    "metadata": {},
2499:    "outputs": [
2500:     {
2501:      "data": {
2502:       "text/html": [
2503:        "<div>\n",
2504:        "<style scoped>\n",
2505:        "    .dataframe tbody tr th:only-of-type {\n",
2506:        "        vertical-align: middle;\n",
2507:        "    }\n",
2508:        "\n",
2509:        "    .dataframe tbody tr th {\n",
2510:        "        vertical-align: top;\n",
2511:        "    }\n",
2512:        "\n",
2513:        "    .dataframe thead th {\n",
2514:        "        text-align: right;\n",
2515:        "    }\n",
2516:        "</style>\n",
2517:        "<table border=\"1\" class=\"dataframe\">\n",
2518:        "  <thead>\n",
2519:        "    <tr style=\"text-align: right;\">\n",
2520:        "      <th></th>\n",
2521:        "      <th>review</th>\n",
2522:        "      <th>text_length</th>\n",
2523:        "      <th>word_count</th>\n",
2524:        "      <th>sentence_count</th>\n",
2525:        "    </tr>\n",
2526:        "  </thead>\n",
2527:        "  <tbody>\n",
2528:        "    <tr>\n",
2529:        "      <th>0</th>\n",
2530:        "      <td>my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...</td>\n",
2531:        "      <td>204</td>\n",
2532:        "      <td>40</td>\n",
2533:        "      <td>1</td>\n",
2534:        "    </tr>\n",
2535:        "    <tr>\n",
2536:        "      <th>1</th>\n",
2537:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2538:        "      <td>889</td>\n",
2539:        "      <td>169</td>\n",
2540:        "      <td>1</td>\n",
2541:        "    </tr>\n",
2542:        "    <tr>\n",
2543:        "      <th>2</th>\n",
2544:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2545:        "      <td>522</td>\n",
2546:        "      <td>107</td>\n",
2547:        "      <td>1</td>\n",
2548:        "    </tr>\n",
2549:        "    <tr>\n",
2550:        "      <th>3</th>\n",
2551:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2552:        "      <td>2489</td>\n",
2553:        "      <td>487</td>\n",
2554:        "      <td>1</td>\n",
2555:        "    </tr>\n",
2556:        "    <tr>\n",
2557:        "      <th>4</th>\n",
2558:        "      <td>my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried</td>\n",
2559:        "      <td>153</td>\n",
2560:        "      <td>32</td>\n",
2561:        "      <td>1</td>\n",
2562:        "    </tr>\n",
2563:        "  </tbody>\n",
2564:        "</table>\n",
2565:        "</div>"
2566:       ],
2567:       "text/plain": [
2568:        "                                                                                                                                                                                                    review  \\\n",
2569:        "0  my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...   \n",
2570:        "1  the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2571:        "2  very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2572:        "3  i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2573:        "4                                                my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried   \n",
2574:        "\n",
2575:        "   text_length  word_count  sentence_count  \n",
2576:        "0          204          40               1  \n",
2577:        "1          889         169               1  \n",
2578:        "2          522         107               1  \n",
2579:        "3         2489         487               1  \n",
2580:        "4          153          32               1  "
2581:       ]
2582:      },
2583:      "execution_count": 272,
2584:      "metadata": {},
2585:      "output_type": "execute_result"
2586:     }
2587:    ],
2588:    "source": [
2589:     "#feature engineering for yelp\n",
2590:     "\n",
2591:     "yelp_sample[\"text_length\"] = yelp_sample[\"review\"].str.len()\n",
2592:     "\n",
2593:     "yelp_sample[\"word_count\"] = yelp_sample[\"review\"].str.split().apply(len)\n",
2594:     "\n",
2595:     "yelp_sample[\"sentence_count\"] = yelp_sample[\"review\"].apply(\n",
2596:     "    lambda x: len([s for s in nltk.sent_tokenize(x) if s.strip()])\n",
2597:     ")\n",
2598:     "\n",
2599:     "yelp_sample[[\"review\",\"text_length\", \"word_count\", \"sentence_count\"]].head()"
2600:    ]
2601:   },
2602:   {
2603:    "cell_type": "code",
2604:    "execution_count": 273,
2605:    "id": "dd293d5c",
2606:    "metadata": {},
2607:    "outputs": [
2608:     {
2609:      "data": {
2610:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUbpJREFUeJzt3Xd0FWX+x/FPegikQEJLCAk9CBjpKiUSCF0WFlGKIoKKLhZQFmVXsa2L4qK4y1pWBWVdFCxUUQhNioiK9F5CC4FQQkIJkPL8/uAwPy4JcC/c5Abm/Ton52Se+d6Z751c4MPkmRkvY4wRAAAAYCPenm4AAAAAKG6EYAAAANgOIRgAAAC2QwgGAACA7RCCAQAAYDuEYAAAANgOIRgAAAC2QwgGAACA7RCCAVy3xx9/XD169PDo/vr166d+/foVWw+X66MkWr58uXr06KFbb71VcXFxnm6nUBMnTlRcXJxOnDjh6VZuaD169NAjjzzi6TaAGwIhGICDESNGKC4uTnFxcapbt64aN26s9u3ba9iwYVq4cKEKe8jkvn37lJKS4vK+Bg4cqHvuucfl1xW2vz179mjPnj0ub+tqrtTjtb7v4pSamqqkpCRFRkbqf//7n6ZPn37Z2ot/9nFxcbr11lvVuXNnvf/++8rNzS3SPo8ePaqtW7cqLy+vSPdzNV9//bXi4uK0bNkyj/ZxJb1791b//v0LXZeSkqJ9+/YVc0fAjcnX0w0AKFkOHDigrVu3au3atfL399fZs2e1f/9+JScnq1u3boqPj9fUqVMVFRVlveaDDz64ppC0d+9eHT9+3OXXXev+rsWVeizOPq7VggULlJ2drWeffVbVq1e/Yu2lP/usrCzNmTNHTzzxhObNm6dp06YVWZ8DBw5U165dFRISUmT7cMbx48e1detWnTx50qN9XMnu3bsVGBjo6TaAGx4hGEChateubf1DGx8fry5duujhhx9WixYt1KVLF61atUo+Pj6SpCpVqhRrb8W9v8spKX1cycGDByXJpXB58c++WbNm2rFjh/73v/9p7dq1io+PL5I+y5Urp3LlyhXJtgGgMEyHAOC0+vXr6/nnn9fatWv1zTffWOOFzY3du3evhg0bptatW6tp06a6//77HX7F3KFDB61YsUIbN260fv3euHFja/2FOb6ZmZl69tln1bRpUz399NOX3d8FGRkZevLJJ9W4cWMlJiZq4sSJBWratm2rZ599tsD4iy++qDvuuMPpHi/Xx88//6x+/fqpYcOGatasmZ566int3bvXoebC+zt58qSGDx+uJk2aKCEhQRMmTCj0fRXmavu544479I9//MP6Pi4uTi+//LLT27+gUaNGkqRt27Y5jGdmZur111/XXXfdpVtvvVVdu3Z1+FxMnTpVcXFxWrNmTYFtLlmyRHFxcUpOTpZ0+TnBV9vH6tWrFRcXpyVLllhj+/fvV1xcnFq2bOmwrXHjxunWW2/V2bNnXT4Gl9qyZYv+9Kc/qVmzZmrYsKEGDBigjRs3OtRcmJ97/PhxPf3002rcuLHatGmjyZMnF7rNb775Rh06dFDDhg310EMPad++fRoxYoTuuusuq6ZVq1Zau3atfvnlF+sz2apVqwLbcnafgJ0RggG4pFu3bpKkuXPnWmOXzo3NyspSy5YttW7dOr344ov6z3/+o65du+qFF17Q77//Lkl6//33FR8frxo1amj69OmaPn26vvjiC2sbe/bs0a5du9S3b1/Vr19f77zzjmJiYgrd3wV5eXnq16+fmjZtqvfff18JCQl6+OGH9de//tWhbufOnUpNTS3w+rS0NG3fvt1avlqPhfUxZcoUK3y9++67evnll7VixQo1bNhQmzZtKvD+BgwYoAYNGuj9999X8+bNNWjQIE2ZMuVyh9+l/fz3v//VAw88YH0/ffp0Pf7441fd9qUOHDggSSpfvrw1dujQITVp0kSTJk3S448/rgkTJigxMVH3... (line truncated to 2000 chars)
2611:       "text/plain": [
2612:        "<Figure size 800x500 with 1 Axes>"
2613:       ]
2614:      },
2615:      "metadata": {},
2616:      "output_type": "display_data"
2617:     }
2618:    ],
2619:    "source": [
2620:     "plt.figure(figsize=(8,5))\n",
2621:     "\n",
2622:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"word_count\"], bins=40, alpha=0.6, label=\"Genuine\")\n",
2623:     "\n",
2624:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"word_count\"], bins=40, alpha=0.6, label=\"AI Generated\")\n",
2625:     "\n",
2626:     "plt.xlabel(\"Word Count\")\n",
2627:     "plt.ylabel(\"Frequency\")\n",
2628:     "plt.title(\"Distribution of Review Length\")\n",
2629:     "plt.legend()\n",
2630:     "\n",
2631:     "plt.show()"
2632:    ]
2633:   },
2634:   {
2635:    "cell_type": "code",
2636:    "execution_count": 274,
2637:    "id": "4ced490d",
2638:    "metadata": {},
2639:    "outputs": [
2640:     {
2641:      "data": {
2642:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsQAAAHVCAYAAAD2N+0gAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATPBJREFUeJzt3Xd0FXX+//HXTSVACoSaEEIvSlm6irTQq7CiNFEEFRX3SxFZcJVVV8WyKKzYVsGyCoLSFAtNkCIgIL2DgYSQECAhoQRI+fz+4GR+XhIgN9ybBOb5OCfncD/znvm8bybBl8PnzjiMMUYAAACATXkVdgMAAABAYSIQAwAAwNYIxAAAALA1AjEAAABsjUAMAAAAWyMQAwAAwNYIxAAAALA1AjEAAABsjUAM4IY98cQT6tOnT6HON2jQIA0aNKjAerhaH0XR2rVr1adPHzVo0EB16tQp7HZy9cknn6hOnTo6c+ZMYbdyU+vTp48effTRwm4DuOkQiAE4GTdunOrUqaM6deqobt26atKkiTp16qTRo0fr559/Vm4Pt4yNjVV0dLTLcw0dOlR9+/Z1eb/c5jty5IiOHDni8rGu51o95vd9F6S4uDh17NhRYWFh+vLLL7VgwYKr1v753NepU0cNGjRQt27d9P777ysjI8OjfZ46dUr79u1TZmamR+e5nm+++UZ16tTRmjVrCrWPa+nfv78efPDBXLdFR0crNja2gDsCbn4+hd0AgKLl2LFj2rdvn7Zt2yY/Pz9dvHhRR48e1dKlS9WrVy81bNhQc+bMUXh4uLXPBx98kK/AFBMTo9OnT7u8X37ny49r9ViQfeTX8uXLlZaWpqefflrVqlW7Zu2V5z41NVU//PCDnnrqKS1ZskTz58/3WJ9Dhw5Vjx49FBQU5LE58uL06dPat2+fzp49W6h9XMvhw4dVrFixwm4DuKUQiAHkqlatWtZ/dBs2bKju3bvrkUceUcuWLdW9e3dt3rxZ3t7ekqRKlSoVaG8FPd/VFJU+riUhIUGSXAqafz73zZs318GDB/Xll19q27ZtatiwoUf6LF26tEqXLu2RYwPA9bBkAkCe1atXT+PHj9e2bds0d+5cazy3tbQxMTEaPXq0WrdurWbNmumBBx5w+mfozp07a926ddq1a5f1T/RNmjSxtmevCU5JSdHTTz+tZs2aaeTIkVedL1tycrL+9re/qUmTJoqKitInn3ySo6Z9+/Z6+umnc4w///zzuvPOO/Pc49X6WL9+vQYNGqRGjRqpefPm+r//+z/FxMQ41WS/v7Nnz2rs2LFq2rSp2rRpoxkzZuT6vnJzvXnuvPNO/fvf/7b+XKdOHb3wwgt5Pn62xo0bS5L279/vNJ6SkqJXXnlFbdu2VYMGDdSjRw+nn4s5c+aoTp062rp1a45jrlq1SnXq1NHSpUslXX0N8fXm2LJli+rUqaNVq1ZZY0ePHlWdOnV09913Ox1rypQpatCggS5evOjy9+BKe/fu1ZNPPqnmzZurUaNGGjJkiHbt2uVUk72e9/Tp0xo5cqSaNGmidu3aaebMmbkec+7cuercubMaNWqkhx9+WLGxsRo3bpzatm1r1bRq1Urbtm3Tb7/9Zv1MtmrVKsex8jongMsIxABc0qtXL0nS4sWLrbEr19Kmpqbq7rvv1vbt2/X888/rv//9r3r06KHnnntOv//+uyTp/fffV8OGDVW9enUtWLBACxYs0KxZs6xjHDlyRH/88YcGDhyoevXq6e2331ZkZGSu82XLzMzUoEGD1KxZM73//vtq06aNHnnkEf3jH/9wqjt06JDi4uJy7B8fH68DBw5Yr6/XY259zJ492wpiU6dO1QsvvKB169apUaNG2r17d473N2TIENWvX1/vv/++WrRooWHDhmn27NlX+/a7NM///vc/DR482PrzggUL9MQTT1z32Fc6duyYJKls2bLW2PHjx9W0aVN9/vnneuKJJzRjxgxFRUXp... (line truncated to 2000 chars)
2643:       "text/plain": [
2644:        "<Figure size 800x500 with 1 Axes>"
2645:       ]
2646:      },
2647:      "metadata": {},
2648:      "output_type": "display_data"
2649:     }
2650:    ],
2651:    "source": [
2652:     "plt.figure(figsize=(8,5))\n",
2653:     "\n",
2654:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"word_count\"], bins=40, alpha=0.6, label=\"Genuine\")\n",
2655:     "\n",
2656:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"word_count\"], bins=40, alpha=0.6, label=\"AI Generated\")\n",
2657:     "\n",
2658:     "plt.xlabel(\"Word Count\")\n",
2659:     "plt.ylabel(\"Frequency\")\n",
2660:     "plt.title(\"Distribution of Review Length\")\n",
2661:     "plt.legend()\n",
2662:     "\n",
2663:     "plt.show()"
2664:    ]
2665:   },
2666:   {
2667:    "cell_type": "code",
2668:    "execution_count": 275,
2669:    "id": "487b66a7",
2670:    "metadata": {},
2671:    "outputs": [
2672:     {
2673:      "data": {

(Output capped at 50 KB. Showing lines 1471-2673. Use offset=2674 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 2.8s)

_Thinking:_

Let me continue reading the rest of the notebook.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 2674
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
2674:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAh0AAAHCCAYAAABL4HuAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAARO5JREFUeJzt3Xl8TXf+x/F39k0WYicEsQSxhCKkTVCttYqWttYZ1c20QzsL03aqNa3+ZjrVxWhNdbRqiX1a2qGoFC1K7BVLtZEIgiBBIuv5/WFyx5WEm7g5N67X8/G4j/Z+z+d87+ckkvvO2a6LYRiGAAAAKpiroxsAAAB3BkIHAAAwBaEDAACYgtABAABMQegAAACmIHQAAABTEDoAAIApCB0AAMAUhA7gNrJixQqtWbPG0W2gEpk3b56+++47R7cB2MSFO5IC//Ptt9/qyJEjGjVqlDw9Pa2WLVu2TOfPn9fQoUMVEBBgtezLL79Uenq6Ro0aVaH9tWvXTrVr19bq1attXicpKUm7d+/WxYsXVadOHTVt2lQNGzaswC7L7tNPP1WzZs0UFRVV5nVvh+2rSNWrV9dDDz2kDz/80NGtADfFng7gGj/88IPGjRunrVu3Wo1nZ2frscce07hx47Ru3TqrZYZhaPTo0frnP/9pZqs3tXv3bkVHR6tly5b6xz/+obVr12ratGlq2rSp7r77biUkJDi6RYvx48dr/vz5ZVrndtq+ijRy5EhFR0c7ug3AJoQO4Bo9evSQJG3YsMFqfPPmzcrNzVV4eLi++eYbq2V79uxRenq6Zd3KYOvWreratauqVKmipKQkrV27VnPnztX69ev1888/y8/PT1u2bHF0m+Xm7NtXFtOnT9eIESMc3QZgE3dHNwBUJu3bt1fVqlX1zTff6JVXXrGMf/PNNwoPD9fQoUO1ePFiq3WKQsj1oePHH3/Unj175Orqqg4dOqhp06ZWy9etW6cLFy7ooYceUlpamjZt2iQfHx/169dPknTp0iVt2LBBly9fVteuXdWgQQObtqGgoEAjR45UzZo1tWzZMvn5+Vktr1+/vlatWqVDhw5Zjefl5WnLli06duyYAgMDFR0drWrVqlmWZ2dna/78+YqKilKrVq2s1l2+fLmqVKmi++67zzL2r3/9S61bt1anTp20d+9e7d27V/Xq1VNMTIxcXa/+vZOTk6PPPvtM+fn5OnDggGbPni1Jqlevnvr06WPq9l3f886dO3Xw4EG1bt1abdq0sdTs2rVLBw4cUOPGjUs8HHTtHAkJCUpMTFSDBg0UHR1t2e5rv27nzp2TJLm7u6tWrVrq1q1bscN31865b98+7dmzR23btlVERITmzZunRo0aqVu3blbr7Nu3T4cOHZKbm5vatm2rxo0bF+u1rF+T0r6PgM0MAFYGDRpkeHp6GllZWZaxTp06Gc8884yxYcMGQ5Jx8uRJy7L+/fsbPj4+xpUrVwzDMIyMjAyjX79+ho+Pj9GnTx+jV69ehqenp/Hoo48a2dnZlvUGDhxoNG/e3FiwYIERERFhDBo0yOjbt69hGIbx3XffGTVr1jQaNGhgPPzww0abNm2Mjz/+2Gjbtq1x//3337D/NWvWGJKMv/zlLzZv886dO43GjRsbderUMR566CGjffv2ho+Pj/H+++9bak6ePGlIMqZPn15s/VatWhn9+vWzGnNzczNeeOEF4ze/+Y0RExNjDBo0yPDz8zOio6ONnJwcwzAM4+LFi8bYsWMNd3d3o2XLlsbYsWONsWPHGn//+99N375rex47dqzRs2dPo3///oa7u7vx6quvGvn5+caYMWOMHj16GAMGDDDc3NyMp556qthrubm5Gc8//7wxZswYIyYmxhg4cKAREBBgdOnSxTh79qxV7Z///GfLNj/22GNGeHi4UaVKFWP58uUl9vX4448bd999t3Hvvfcab731lmEYhhEcHGw8+eSTltrs7GzjvvvuMwIDA41B... (line truncated to 2000 chars)
2675:       "text/plain": [
2676:        "<Figure size 600x500 with 1 Axes>"
2677:       ]
2678:      },
2679:      "metadata": {},
2680:      "output_type": "display_data"
2681:     }
2682:    ],
2683:    "source": [
2684:     "plt.figure(figsize=(6,5))\n",
2685:     "\n",
2686:     "plt.boxplot(\n",
2687:     "    [\n",
2688:     "        amazon_df[amazon_df[\"label\"] == 0][\"word_count\"],\n",
2689:     "        amazon_df[amazon_df[\"label\"] == 1][\"word_count\"]\n",
2690:     "    ],\n",
2691:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
2692:     ")\n",
2693:     "\n",
2694:     "plt.ylabel(\"Word Count\")\n",
2695:     "plt.title(\"Word Count Comparison\")\n",
2696:     "\n",
2697:     "plt.show()"
2698:    ]
2699:   },
2700:   {
2701:    "cell_type": "code",
2702:    "execution_count": 276,
2703:    "id": "b8fb915d",
2704:    "metadata": {},
2705:    "outputs": [
2706:     {
2707:      "data": {
2708:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAiYAAAHCCAYAAADb8wJPAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUEVJREFUeJzt3XlcVPX+P/DXzLCDoLK5sSkaCKhoueDCYm6ooWia5XavqZXde8vqqrdNb92491ZS125pWZrmErnUdV8SChdMScQdIhFBBEQFlJ35/P7gN+fLCOoAh5lh5vV8PObRzPm858x7oHHefM5nUQghBIiIiIiMgNLQCRARERFpsDAhIiIio8HChIiIiIwGCxMiIiIyGixMiIiIyGiwMCEiIiKjwcKEiIiIjAYLEyIiIjIaLEyITMz27duxb98+Q6dBRuSbb77BkSNHDJ0GkU4UXPmVqHF++uknpKenY+bMmbCystJq27p1K27duoUpU6bA0dFRq23Xrl0oLCzEzJkzWzS/Pn36oEOHDti7d6/Oz8nMzERKSgpKSkrQsWNHdO/eHV5eXi2YZeN9/fXX6NGjBwYNGtTo57aG99eSXFxcMHnyZKxcudLQqRA9FHtMiBrpl19+wdy5c5GUlKR1vKysDE8//TTmzp2LgwcParUJITBr1ix8/vnn+kz1oVJSUjBkyBD07NkT//3vf3HgwAHExMSge/fuGDp0KJKTkw2domTBggXYsGFDo57Tmt5fS5oxYwaGDBli6DSIdMLChKiRIiIiAADx8fFaxw8fPozKykr4+/vj0KFDWm2nT59GYWGh9FxjkJSUhJCQEDg4OCAzMxMHDhzAunXr8OOPP+L333+Hvb09jh07Zug0m8zU319jxMbGYvr06YZOg0gnFoZOgKi1CQ4ORrt27XDo0CG8/fbb0vFDhw7B398fU6ZMQVxcnNZzNIXKvYXJuXPncPr0aSiVSvTr1w/du3fXaj948CBu376NyZMnIy8vD4mJibC1tcXYsWMBAHfu3EF8fDzu3r2LkJAQeHp66vQeampqMGPGDLi5uWHr1q2wt7fXau/SpQt27tyJS5cuaR2vqqrCsWPHcOXKFTg5OWHIkCFo37691F5WVoYNGzZg0KBBCAgI0Hrutm3b4ODggJEjR0rHvvrqKwQGBqJ///5ITU1FamoqOnfujNDQUCiVtX83VVRUYP369aiursb58+exevVqAEDnzp0xZswYvb6/e3P+9ddfcfHiRQQGBqJXr15SzKlTp3D+/Hl07dq1wUtPdc+RnJyMCxcuwNPTE0OGDJHed92f282bNwEAFhYWcHd3x+DBg+tdKqx7zjNnzuD06dPo3bs3goKC8M0338DHxweDBw/Wes6ZM2dw6dIlqFQq9O7dG127dq2Xa2N/Jvf7PRLpTBBRo02cOFFYWVmJ0tJS6Vj//v3FCy+8IOLj4wUAkZubK7WNGzdO2NraivLyciGEEEVFRWLs2LHC1tZWjBkzRowYMUJYWVmJadOmibKyMul5UVFR4pFHHhEbN24UQUFBYuLEiSIyMlIIIcSRI0eEm5ub8PT0FE8++aTo1auX+PLLL0Xv3r3FqFGjHpj/vn37BADx7rvv6vyef/31V9G1a1fRsWNHMXnyZBEcHCxsbW3FihUrpJjc3FwBQMTGxtZ7fkBAgBg7dqzWMZVKJV555RXx4osvitDQUDFx4kRhb28vhgwZIioqKoQQQpSUlIg5c+YICwsL0bNnTzFnzhwxZ84c8eGHH+r9/dXNec6cOWL48OFi3LhxwsLCQixbtkxUV1eL2bNni4iICDF+/HihUqnEc889V++1VCqVWLhwoZg9e7YIDQ0VUVFRwtHRUQwcOFDcuHFDK/att96S3vPTTz8t/P39hYODg9i2bVuDeT377LNi6NCh4vHHHxcffPCBEEIIZ2dnMX/+fCm2rKxMjBw5Ujg5OYmJEyeKJ598UvTo0UNMmTKlWT+T... (line truncated to 2000 chars)
2709:       "text/plain": [
2710:        "<Figure size 600x500 with 1 Axes>"
2711:       ]
2712:      },
2713:      "metadata": {},
2714:      "output_type": "display_data"
2715:     }
2716:    ],
2717:    "source": [
2718:     "plt.figure(figsize=(6,5))\n",
2719:     "\n",
2720:     "plt.boxplot(\n",
2721:     "    [\n",
2722:     "        yelp_sample[yelp_sample[\"label\"] == 0][\"word_count\"],\n",
2723:     "        yelp_sample[yelp_sample[\"label\"] == 1][\"word_count\"]\n",
2724:     "    ],\n",
2725:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
2726:     ")\n",
2727:     "\n",
2728:     "plt.ylabel(\"Word Count\")\n",
2729:     "plt.title(\"Word Count Comparison\")\n",
2730:     "\n",
2731:     "plt.show()"
2732:    ]
2733:   },
2734:   {
2735:    "cell_type": "code",
2736:    "execution_count": 277,
2737:    "id": "bf96bddf",
2738:    "metadata": {},
2739:    "outputs": [
2740:     {
2741:      "data": {
2742:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUvVJREFUeJzt3Xd4VGX6xvE7CekVAhhCEnoTqUESxEKXmiCyiygsq4iICijYUBBRabquorurCC4qrrDSOygQEBHpiEiTCCGAgYQ00tv5/cGPWYccIAMTJiHfz3XNdTHvec57npkJeHvyzjlOhmEYAgAAAGDF2dENAAAAAGURQRkAAAAwQVAGAAAATBCUAQAAABMEZQAAAMAEQRkAAAAwQVAGAAAATBCUAQAAABMEZQBAubBu3TotW7bMocdbvny5Vq1addN6uFIfAG4OJ+7MB8CefvnlFx07dky5ubmqX7++WrRoIRcXl1I/7qpVq1RYWKioqKhSP9bNlpSUpJ07dyopKUmBgYGqXbu2br/9dke3ZcXW9z8mJkaxsbGSJCcnJ3l5eSkwMFB33HGHgoODTffp3r27kpKStGvXrlLt7WrHi4yMlIeHhzZt2mTTXDfS4/W+bgA3rpKjGwBwazhy5Igef/xx7d69Wx06dFBAQIC+//57GYahcePG6amnnirV47/zzjvKycm5pYJyQkKCRo0apaVLl6pNmzaqV6+eUlNTtXnzZgUHB2vKlCnq16+fo9uUZPv7P3PmTP33v//VY489JicnJ+Xm5urUqVPasWOHGjdurAkTJqhv375W+3Tv3l0ZGRml3tuNHu96XK3Hm9kHAGsEZQA3zDAMRUVFKSsrS7/++qtq1qwpSSooKNDUqVM1f/78Ug/Kt5qEhAS1bdtWXl5e2rdvn9UZ5IyMDL388stasWJFmQnK12vmzJmqVOl//ylKTU3Vyy+/rAceeEDTp0/Xiy++aNn27LPP3tTebvbxrqSs9AFURARlADfsyJEjOnr0qMaOHWsJyZJUqVIlTZgwQb179zbd7/jx49q1a5fy8vJ0xx13qEWLFlbbly9fLhcXF/Xq1UsnT57U1q1b5evrq06dOsnLy8tS99///le///67CgoKNHv2bEmSu7u7Bg8eXCrH+6OTJ09q586dKiwsVKtWrdSgQQObX6eZkSNHKiEhQb/88kuxOX18fPSPf/xDP/30U7H99uzZo0OHDsnNzU1t27ZVrVq1rLbPmzdPNWrUUIcOHazGv/vuO506dUoPP/ywze9HSd//kggICNDHH3+sEydO6NVXX1W/fv1Uv359SRfX6ubk5Cg6Otpqn7i4OO3bt085OTlq3Lix1ft7rd4uf43btm1T9erV1bFjxyse75LY2Fht375dAQEB6tixozw9Pa22l/S9vlaPV+vjWp/39fxMA/gDAwBu0OnTpw1JxuDBg0tUn5GRYQwcONBwc3MzunbtavTr188ICAgw+vTpY1y4cMFSFxERYdx3333GrFmzjPDwcONPf/qTcdtttxm1atUy4uPjLXUvvfSSERQUZFSrVs0YOnSoMXToUGPkyJGldjzDMIwLFy4YDz/8sOHq6mrcc889xp///GejcePGxsMPP2zzcS+XmJhoODs7G3379i3R+2kYhpGQkGDcfffdhq+vrxEVFWV07NjRqFSpkvHUU08ZBQUFlrqaNWsajzzySLH9hwwZYtx2221WY/Z6/80MGDDAkGTk5+ebbl+5cqUhyXjjjTcsY/fff78RHh5uVffss88anp6eRvfu3Y2HH37YaN26tdG+fXsjISGhRL1deo0ffPCB0apVKyMqKsr4y1/+csXjXar/+9//brRu3dro37+/ERwcbISGhhr79++3qi3pe32tHs36KOnnbcvPNIDiCMoA7KJnz56Gs7OzMWrUKGPbtm1Gdnb2FWsHDhxo+Pj4GHv37rWMxcXFGbfddpsxbNgwy1hERIRRs2ZNY9y4cZax... (line truncated to 2000 chars)
2743:       "text/plain": [
2744:        "<Figure size 800x500 with 1 Axes>"
2745:       ]
2746:      },
2747:      "metadata": {},
2748:      "output_type": "display_data"
2749:     }
2750:    ],
2751:    "source": [
2752:     "plt.figure(figsize=(8,5))\n",
2753:     "\n",
2754:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"sentence_count\"], bins=25, alpha=0.6, label=\"Genuine\")\n",
2755:     "\n",
2756:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"sentence_count\"], bins=25, alpha=0.6, label=\"AI Generated\")\n",
2757:     "\n",
2758:     "plt.title(\"Sentence Count Distribution\")\n",
2759:     "plt.xlabel(\"Sentence Count\")\n",
2760:     "plt.ylabel(\"Frequency\")\n",
2761:     "plt.legend()\n",
2762:     "\n",
2763:     "plt.show()"
2764:    ]
2765:   },
2766:   {
2767:    "cell_type": "code",
2768:    "execution_count": 278,
2769:    "id": "157bae5d",
2770:    "metadata": {},
2771:    "outputs": [
2772:     {
2773:      "data": {
2774:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAASKJJREFUeJzt3XlcVXX+x/E3ILssihog4L5lrphgWrnviqmlpeQ4jKWZZpqZoy3OlEvWmE7zK8vJzEon9zSX3DUzt1wyt0QT1FCQTRQQ4fz+aLzTlaNy5cJFfT0fj/t4dL/ne77fzz0H7e3he89xMgzDEAAAAAArzo4uAAAAACiJCMoAAACACYIyAAAAYIKgDAAAAJggKAMAAAAmCMoAAACACYIyAAAAYIKgDAAAAJggKAMA7ghr1qzRsmXLHDrf119/rW+++abYarhRHQCKhxNP5gNgTz///LOOHz+u7OxsVa9eXQ0aNJCLi0uRz/vNN98oNzdX3bt3L/K5iltSUpJ27dqlpKQkBQQEqHLlyrr//vsdXZYVW4//xo0bFRsbK0lycnKSl5eXAgIC9MADDyg4ONh0n44dOyopKUm7d+8u0tpuNl9kZKQ8PDy0adMmm8YqTI23+7kBFF4pRxcA4O5w9OhR/eUvf9GePXvUsmVL+fv767vvvpNhGBo7dqyee+65Ip1/6tSpysrKuquCckJCgoYPH66lS5eqSZMmqlatmlJTU7V582YFBwdr4sSJ6tmzp6PLlGT78Z85c6b+85//6M9//rOcnJyUnZ2t06dPa+fOnapdu7ZeffVV9ejRw2qfjh07KiMjo8hrK+x8t+NmNRZnHQCsEZQBFJphGOrevbsuX76sX375RRUrVpQkXb16VZMmTdL8+fOLPCjfbRISEtS0aVN5eXlp3759VleQMzIy9Morr2j58uUlJijfrpkzZ6pUqf/9ryg1NVWvvPKKHnvsMU2ZMkUvv/yyZduIESOKtbbinu9GSkodwL2IoAyg0I4ePapjx45p1KhRlpAsSaVKldKrr76qrl27mu538uRJ7d69W1euXNEDDzygBg0aWG3/+uuv5eLioi5duiguLk7btm2Tj4+PWrduLS8vL0u///znP/rtt9909epVzZo1S5Lk7u6u6OjoIpnvj+Li4rRr1y7l5uaqUaNGqlGjhs2f08ywYcOUkJCgn3/+Od+YpUuX1vvvv6/9+/fn2+/HH3/U4cOH5ebmpqZNm6pSpUpW2+fNm6egoCC1bNnSqn3Lli06ffq0nnrqKZuPR0GPf0H4+/vrww8/1K+//qpx48apZ8+eql69uqTf1+pmZWUpKirKap9Tp05p3759ysrKUu3ata2O761qu/4zbt++XRUqVFCrVq1uON81sbGx2rFjh/z9/dWqVSt5enpabS/osb5VjTer41bn+3Z+pgH8gQEAhXTmzBlDkhEdHV2g/hkZGcaTTz5puLm5Ge3atTN69uxp+Pv7G926dTMuXrxo6RcREWE8+uijxscff2yEh4cbjz/+uHHfffcZlSpVMuLj4y39xowZYwQGBhrly5c3YmJijJiYGGPYsGFFNp9hGMbFixeNp556ynB1dTUefvhh44knnjBq165tPPXUUzbPe73ExETD2dnZ6NGjR4GOp2EYRkJCgtGiRQvDx8fH6N69u9GqVSujVKlSxnPPPWdcvXrV0q9ixYpGv3798u0/YMAA47777rNqs9fxN9OnTx9DkpGTk2O6fcWKFYYk429/+5ulrUOHDkZ4eLhVvxEjRhienp5Gx44djaeeespo3Lix0bx5cyMhIaFAtV37jDNmzDAaNWpkdO/e3Xj66advON+1/v/4xz+Mxo0bG7179zaCg4ON0NBQ48CBA1Z9C3qsb1WjWR0FPd+2/EwDyI+gDMAuOnfubDg7OxvDhw83tm/fbmRmZt6w75NPPmmULl3a2Lt3r6Xt1KlTxn333WcMGjTI0hYREWFUrFjRGDt2... (line truncated to 2000 chars)
2775:       "text/plain": [
2776:        "<Figure size 800x500 with 1 Axes>"
2777:       ]
2778:      },
2779:      "metadata": {},
2780:      "output_type": "display_data"
2781:     }
2782:    ],
2783:    "source": [
2784:     "plt.figure(figsize=(8,5))\n",
2785:     "\n",
2786:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"sentence_count\"], bins=25, alpha=0.6, label=\"Genuine\")\n",
2787:     "\n",
2788:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"sentence_count\"], bins=25, alpha=0.6, label=\"AI Generated\")\n",
2789:     "\n",
2790:     "plt.title(\"Sentence Count Distribution\")\n",
2791:     "plt.xlabel(\"Sentence Count\")\n",
2792:     "plt.ylabel(\"Frequency\")\n",
2793:     "plt.legend()\n",
2794:     "\n",
2795:     "plt.show()"
2796:    ]
2797:   },
2798:   {
2799:    "cell_type": "code",
2800:    "execution_count": 279,
2801:    "id": "702ddf2b",
2802:    "metadata": {},
2803:    "outputs": [],
2804:    "source": [
2805:     "def vocab_richness(text):\n",
2806:     "    words = text.split()\n",
2807:     "    if len(words) == 0:\n",
2808:     "        return 0\n",
2809:     "    return len(set(words)) / len(words)\n",
2810:     "\n",
2811:     "amazon_df[\"vocab_richness\"] = amazon_df[\"review\"].apply(vocab_richness)"
2812:    ]
2813:   },
2814:   {
2815:    "cell_type": "code",
2816:    "execution_count": 280,
2817:    "id": "c57b8d36",
2818:    "metadata": {},
2819:    "outputs": [
2820:     {
2821:      "data": {
2822:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATLZJREFUeJzt3Xd4FFX//vF7SSWQRkIJSAkdROkgRUFpQUSaEgQBBRQRFdBHFAvw+Kio2LtSrSC9qICgIkVAEKRJJxBCL4EEElLP7w9+2S9LCruwKWTer+vKdbFnzsx8pqy5nZyZsRljjAAAAAALKZLfBQAAAAB5jRAMAAAAyyEEAwAAwHIIwQAAALAcQjAAAAAshxAMAAAAyyEEAwAAwHIIwQAAALAcQjCAPNekSRONHTvW7ctt06aNRo4c6fbl5qVr3Ybc2qc3qrw+F7JaX34ck8LwHQDyCiEYKGTatGmj9u3b59hn9OjRqlWrlmJiYvKoKke7d+/WsWPH3L7cffv26ciRI25f7vXo1q2batasqZo1a6pWrVqqX7++evTooVmzZmXZ/1q3Ibf2aUFw+T6sXbu2GjdurHvuuUcvvviiNm7cmOU817ofb7/9do0aNcrl+bJaX24dk5xqLIjfAaCg8szvAgC412233abXX39da9asUbNmzTJNT0pK0scff6zatWvrpptuyocKrSUqKkqJiYlasmSJJOnUqVOaMmWK7r//fr300kv63//+59D/119/lZ+fX36UWmBduQ8TEhIUFRWlBQsWqHHjxurRo4emTp3qsN+udT/u2bNHVapUcXm+vDxuOdXI+QM4jxAMFDIDBw7UuHHjNGnSpCxD8OzZsxUbG6tHHnkkH6qzJi8vL9WsWdP+uUWLFtq4caPGjx+vUaNGOYSWawlgVnDlPmzQoIF69Oih+++/X126dJGHh4emTZtmn57X+7GgHLeCUgdwI2A4BFDIVK5cWXfddZd++OEHnT9/PtP0iRMnKiAgQPfff7+9bf78+eratavq1q2rli1basyYMTp79mymedevX6+BAweqcePGatGihZ599lmdOnXKPr1Xr172P1vXqVNHd955p1577TVduHAhy1r37dunvn37qn79+urUqZMWL17sMD0hIUE1a9bU559/nmneXr16qV+/flfdH87WlDF+88CBAxo4cKDq16+vjz/+WN26dVO3bt2yXPagQYPUunVrGWOuWsflbDab6tevr6SkJB08eNBhWnZjOq+27zPExMTY64+IiLBfPc1qW53pK0l//fWX+vfvr4YNG6pRo0YaOnSooqOjHfps3rxZAwcOVLNmzdS8eXMNHjxYO3fudLmPq+655x716tVL06dP1/bt2+3tWe3HnNafnJysmjVr6tSpU5o7d679nOnVq1em/XblOZLd+jK46zx3psbs6nDmO+7qeQHc8AyAQmf69OlGkpk4caJD+759+4zNZjNDhgyxt40ZM8bYbDbz7LPPmjVr1pgffvjBlC9f3lSvXt2cPn3a3m/ChAmmSJEipnfv3mbx4sXmzz//NG+//bbp1KmTvc+BAwfMjh07zI4dO8ymTZvM1KlTTYUKFUyHDh0c6ggMDDT33Xefad26tZk7d65ZtWqVGTRokLHZbOa7776z94uPjzeSzP/+979M29i0aVPTqlUrh7aKFSuaPn36OLRdS02zZ882S5cuNZMnTzYffvihkWQ2btzo0D86Otp4eHiYZ599NqtDYFe3bl1TpUqVTO0dOnQwkszJkyevug3O7PvAwEATGRlpIiIizNy5c82ff/5pevbsaTw8PMzmzZszbauzfSdPnmw8PDzMoEGDzO+//25+//13c88995jQ0FCzd+9eY4wxO3fuNMWKFTP9+vUzK1euNH/99ZeZOHGiueWWW8yFCxec7uPqPsyQcb6/++672e7Hq60/PT3d7Nixw4SGhpquXbvaz5kDBw447LeszpHsjpu7z3Nnasyq... (line truncated to 2000 chars)
2823:       "text/plain": [
2824:        "<Figure size 800x500 with 1 Axes>"
2825:       ]
2826:      },
2827:      "metadata": {},
2828:      "output_type": "display_data"
2829:     }
2830:    ],
2831:    "source": [
2832:     "plt.figure(figsize=(8,5))\n",
2833:     "\n",
2834:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"vocab_richness\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
2835:     "\n",
2836:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"vocab_richness\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
2837:     "\n",
2838:     "plt.xlabel(\"Vocabulary Richness\")\n",
2839:     "plt.ylabel(\"Frequency\")\n",
2840:     "plt.title(\"Vocabulary Richness Distribution\")\n",
2841:     "plt.legend()\n",
2842:     "\n",
2843:     "plt.show()"
2844:    ]
2845:   },
2846:   {
2847:    "cell_type": "code",
2848:    "execution_count": 281,
2849:    "id": "8982b997",
2850:    "metadata": {},
2851:    "outputs": [],
2852:    "source": [
2853:     "def vocab_richness(text):\n",
2854:     "    words = text.split()\n",
2855:     "    if len(words) == 0:\n",
2856:     "        return 0\n",
2857:     "    return len(set(words)) / len(words)\n",
2858:     "\n",
2859:     "yelp_sample[\"vocab_richness\"] = yelp_sample[\"review\"].apply(vocab_richness)"
2860:    ]
2861:   },
2862:   {
2863:    "cell_type": "code",
2864:    "execution_count": 282,
2865:    "id": "61457883",
2866:    "metadata": {},
2867:    "outputs": [
2868:     {
2869:      "data": {
2870:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAVdJJREFUeJzt3Xd4FdX+/v07PQRIoYUQAoQaiqJUKUrv0pEiAgoo+rWAnWABzzmKYsGuRwFRUZAqTVBAEEJHOUivARJagIQkQAgp6/mDh/1zk8IO2Slk3q/rynXYa9bMfPY4+3CzsvYaF2OMEQAAAGAhrgVdAAAAAJDfCMEAAACwHEIwAAAALIcQDAAAAMshBAMAAMByCMEAAACwHEIwAAAALIcQDAAAAMshBAPId02aNNGECROcftx27drppZdecvpx89Otvoe8uqa3q/y+FzI7X0H8NykKnwEgvxCCgSKmXbt26tixY7Z9Xn/9ddWuXVvR0dH5VJW9AwcO6PTp004/7uHDh3Xy5EmnHzc3evfurbCwMIWFhal27dq6++671bdvX82dOzfT/rf6HvLqmhYG/7yGderUUePGjXX//ffrlVde0V9//ZXpPrd6He+9916Fh4fneL/MzpdX/02yq7EwfgaAwsq9oAsA4Fz33HOP3nrrLW3cuFHNmjXLsD05OVmffvqp6tSpo4oVKxZAhdYSGRmppKQk/frrr5Kkc+fO6ZtvvtEDDzygV199Vf/+97/t+q9atUo+Pj4FUWqhdeM1vHz5siIjI7Vo0SI1btxYffv21fTp0+2u261ex4MHD6patWo53i8//7tlVyP3D+A4QjBQxIwYMUITJ07U1KlTMw3B8+bNU1xcnB599NECqM6aPDw8FBYWZnvdokUL/fXXX3r33XcVHh5uF1puJYBZwY3XsEGDBurbt68eeOAB9ezZU25ubpo5c6Zte35fx8Ly362w1AHcDpgOARQxVatWVdu2bfXTTz/p4sWLGbZPmTJFvr6+euCBB2xtCxcuVK9evVS/fn21bNlS48eP14ULFzLsu3XrVo0YMUKNGzdWixYt9OKLL+rcuXO27QMHDrT92rpevXpq06aN3nzzTV26dCnTWg8fPqwhQ4bo7rvvVrdu3bR8+XK77ZcvX1ZYWJi+/PLLDPsOHDhQQ4cOven1cLSm6/M3jx49qhEjRujuu+/Wp59+qt69e6t3796ZHnvkyJFq3bq1jDE3reOfXFxcdPfddys5OVnHjh2z25bVnM6bXfvroqOjbfV37tzZNnqa2Xt1pK8kbdmyRcOGDVPDhg3VqFEjPfnkkzp+/Lhdnx07dmjEiBFq1qyZmjdvrlGjRmnfvn057pNT999/vwYOHKhZs2Zp9+7dtvbMrmN257969arCwsJ07tw5LViwwHbPDBw4MMN1u/Eeyep81znrPnekxqzqcOQzntP7ArjtGQBFzqxZs4wkM2XKFLv2w4cPGxcXF/PEE0/Y2saPH29cXFzMiy++aDZu3Gh++uknExISYmrWrGnOnz9v6/f1118bV1dX8+CDD5rly5ebDRs2mPfee89069bN1ufo0aNm7969Zu/evWb79u1m+vTpplKlSqZTp052dfj5+Zl+/fqZ1q1bmwULFpiIiAgzcuRI4+LiYn744Qdbv8TERCPJ/Pvf/87wHps2bWpatWpl11a5cmUzePBgu7ZbqWnevHlmxYoVZtq0aebjjz82ksxff/1l1//48ePGzc3NvPjii5n9J7CpX7++qVatWob2Tp06GUnm7NmzN30Pjlx7Pz8/M2DAANO5c2ezYMECs2HDBtO/f3/j5uZmduzYkeG9Otp32rRpxs3NzYwcOdKsXr3arF692tx///2mTJky5tChQ8YYY/bt22eKFy9uhg4datatW2e2bNlipkyZYu644w5z6dIlh/vk9Bped/1+/+CDD7K8jjc7f3p6utm7d68pU6aM6dWrl+2eOXr0qN11y+we... (line truncated to 2000 chars)
2871:       "text/plain": [
2872:        "<Figure size 800x500 with 1 Axes>"
2873:       ]
2874:      },
2875:      "metadata": {},
2876:      "output_type": "display_data"
2877:     }
2878:    ],
2879:    "source": [
2880:     "plt.figure(figsize=(8,5))\n",
2881:     "\n",
2882:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"vocab_richness\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
2883:     "\n",
2884:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"vocab_richness\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
2885:     "\n",
2886:     "plt.xlabel(\"Vocabulary Richness\")\n",
2887:     "plt.ylabel(\"Frequency\")\n",
2888:     "plt.title(\"Vocabulary Richness Distribution\")\n",
2889:     "plt.legend()\n",
2890:     "\n",
2891:     "plt.show()"
2892:    ]
2893:   },
2894:   {
2895:    "cell_type": "code",
2896:    "execution_count": 283,
2897:    "id": "242b11d8",
2898:    "metadata": {},
2899:    "outputs": [],
2900:    "source": [
2901:     "def avg_word_length(text):\n",
2902:     "    words = text.split()\n",
2903:     "    if len(words) == 0:\n",
2904:     "        return 0\n",
2905:     "    return np.mean([len(word) for word in words])\n",
2906:     "\n",
2907:     "amazon_df[\"avg_word_len\"] = amazon_df[\"review\"].apply(avg_word_length)"
2908:    ]
2909:   },
2910:   {
2911:    "cell_type": "code",
2912:    "execution_count": 284,
2913:    "id": "9adcc1c9",
2914:    "metadata": {},
2915:    "outputs": [
2916:     {
2917:      "data": {
2918:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAq0AAAHVCAYAAADbxcKaAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAR1VJREFUeJzt3XlcVdX+//E3AoKAguI8z+JsDpVTTjlrWuZA2WB6LdPSspuRebWyNLu3W7euWamhpgkpmvNNTU1NU8u5cMp5AkFAQRnX7w9/7K8nUAHRs4XX8/Hg8fCsvfban33Osd4u1t7bxRhjBAAAANhYAWcXAAAAANwKoRUAAAC2R2gFAACA7RFaAQAAYHuEVgAAANgeoRUAAAC2R2gFAACA7RFaAQAAYHuEVgDIoSlTpqhevXrOLuOOSk1NVUBAgD755JO7etwmTZpo0qRJTjtefjlv4F5CaAVs4Mcff1RAQIBatGihtLQ0Z5djG2vXrlVAQIAWLlyYYVtQUJACAgI0ffr0DNumTJmigIAAHT169I7WFxERofDw8Fv2mzBhggICAhQTE3NH67kd9erV05QpUzK0G2N04MABRUZG5njstm3bKiAgQAEBAapTp47uv/9+PfLII5owYYJ+//33TPc5cOCAzp8/n+1j3eg8buWvx8uN876Rm9WY0/MG8gM3ZxcAQPr888915swZHThwQKtWrVK3bt2cXZItNGzYUAcPHtSyZcvUp08fh22hoaE6ceKEFi9erCFDhjhsCwsL08WLF1W5cuW7WO2NnTt3TgcOHFBKSoqzS7mh8PBwRURE3JGxDx8+rOLFi2v+/PmSpMuXL+vIkSNasGCB6tWrp8GDB2vq1Klyd3e39vntt9/k5+eX7WPl9DxyerycuFmNd7MO4F5DaAWcLDIyUt9//73ef/99ff311/rqq68Irf9f8eLFVb9+ff34448O7SdOnNCff/6pwYMHKzQ0VCkpKXJzu/afs0uXLunXX39Vnz595OLi4oyykQlPT08FBARYr5s2bar+/ftr9uzZeuaZZ+Tp6alPP/3U2l6zZs27Wt/dPt6N2KUOwI5YHgA4WXBwsFxdXTVo0CANGzZMy5Yt07lz56ztq1evVkBAgNatW5dh37179yogIEChoaFWW0JCgv71r3+pQ4cOatCggbp06aLZs2c77Dd79mwFBATowoULmjlzptq1a6fatWtLkjZt2mT9Krd27dpq3LixBg4cqE2bNmU4/p9//qnnnntO9913nzp27KilS5dqy5YtCggI0JYtWxz6ZqWuzLRv394KqenWrl2rQoUKacyYMbp06ZJ27Nhhbfvpp5+UkpKi9u3bW22RkZEKCgpSixYt1KhRIz3++OP64YcfHI4zd+5cBQQE6Pz58woODlb79u1Vu3ZtpaamWsfs2bOnGjVqpMDAwCwtC8iu9evX64knntB9992n+++/X6NHj3b4VfH16ywPHz6sgQMHqlGjRurRo4c2b96cYbzU1FR98sknat26tZo1a6bXX39d8fHx6tatm0aMGCFJOn/+vAICApSamqqvv/7a+uyHDRuWYbysHDO7nn76aXXq1EnTpk3TmTNnrPbM1nZu3bpVTz31lB544AG1bt1aL730ko4dO5al87j+vQsPD9fAgQPVsGFDzZ0794bHS7d//371799fjRo1Uu/evbVx40aH7adPn1ZAQIBCQkIy7Nu5c2eNHDkySzXerI558+apR48eatCggdq0aaNJkyYpPj7e2p7d7wZwTzIAnKpWrVrm6aefNsYYExsba3x8fMykSZOs7VeuXDFFixY1/fv3z7Dvyy+/bDw8PExUVJS1f6NGjUzFihXNrFmzzPbt283nn39uihQpYkaNGmXt9+9//9tIMiNHjjR///vfzebNm83o0aONMcZcvnzZ/PHHH+aPP/4wv//+u1m/fr0ZPHiwKVCggNm4caM1xtGjR03x4sVNkyZNzPLly81P... (line truncated to 2000 chars)
2919:       "text/plain": [
2920:        "<Figure size 800x500 with 1 Axes>"
2921:       ]
2922:      },
2923:      "metadata": {},
2924:      "output_type": "display_data"
2925:     }
2926:    ],
2927:    "source": [
2928:     "plt.figure(figsize=(8,5))\n",
2929:     "\n",
2930:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"avg_word_len\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
2931:     "\n",
2932:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"avg_word_len\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
2933:     "\n",
2934:     "plt.title(\"Average Word Length Distribution\")\n",
2935:     "plt.xlabel(\"Average Word Length\")\n",
2936:     "plt.legend()\n",
2937:     "\n",
2938:     "plt.show()"
2939:    ]
2940:   },
2941:   {
2942:    "cell_type": "code",
2943:    "execution_count": 285,
2944:    "id": "cdc4b080",
2945:    "metadata": {},
2946:    "outputs": [],
2947:    "source": [
2948:     "def avg_word_length(text):\n",
2949:     "    words = text.split()\n",
2950:     "    if len(words) == 0:\n",
2951:     "        return 0\n",
2952:     "    return np.mean([len(word) for word in words])\n",
2953:     "\n",
2954:     "yelp_sample[\"avg_word_len\"] = yelp_sample[\"review\"].apply(avg_word_length)"
2955:    ]
2956:   },
2957:   {
2958:    "cell_type": "code",
2959:    "execution_count": 286,
2960:    "id": "57253df7",
2961:    "metadata": {},
2962:    "outputs": [
2963:     {
2964:      "data": {
2965:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArYAAAHVCAYAAAAEi7iFAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUdxJREFUeJzt3Xt8z/X///H7zGyMjc0w50MYOeRYTs0hZ6KIVjo4pANF6UBS+pSWdPLp9KmQUjJJzioJmZxDiJEcZsxmm23Mzs/fH35eX+82bPNm22u36+Xyvlx6P1+P1+v1eL3f7+W+156v19vFGGMEAAAAFHLF8rsBAAAAwBkItgAAALAFgi0AAABsgWALAAAAWyDYAgAAwBYItgAAALAFgi0AAABsgWALAAAAWyDYAsB19NZbb6lRo0b53cZ1lZGRoYCAAE2fPv2G7rdFixYKDg7Ot/0VleMGChOCLVBI/PrrrwoICFDbtm2VmZmZ3+0UGKtXr1ZAQIC+//77LMsmTJiggIAAzZgxI8uyt956SwEBATp8+PB17S8qKkr79++/at3kyZMVEBCgM2fOXNd+rkWjRo301ltvZRk3xigsLEzR0dF53nbHjh0VEBCggIAANWzYUK1bt9add96pyZMn66+//sp2nbCwMJ06dSrX+7rccVzNv/fnjOO+nCv1mNfjBoqC4vndAICc+eSTT3TixAmFhYXpxx9/VK9evfK7pQKhadOmOnDggJYtW6YBAwY4LJs/f76OHTumRYsWacSIEQ7LFi5cqLi4ONWsWfMGdnt5kZGRCgsLU3p6en63cln79+9XVFTUddn233//rfLly2vevHmSpLNnz+rQoUNasGCBGjVqpOHDh+vjjz+Wm5ubtc4ff/yhsmXL5npfeT2OvO4vL67U443sAyhsCLZAIRAdHa3FixfrjTfe0BdffKHPP/+cYPv/lS9fXo0bN9avv/7qMH7s2DH9888/Gj58uObPn6/09HQVL37hf3mJiYnavn27BgwYIBcXl/xoG9nw8PBQQECA9bxly5YaPHiwvvrqKz300EPy8PDQBx98YC2vV6/eDe3vRu/vcgpKH0BBxFQEoBCYPXu2XF1dNXToUD3++ONatmyZIiMjreWrVq1SQECA1qxZk2Xd3bt3KyAgQPPnz7fGkpKS9M4776hLly5q0qSJevTooa+++sphva+++koBAQE6ffq0Zs2apU6dOqlBgwaSpNDQUOvPxg0aNFDz5s01ZMgQhYaGZtn/P//8o2HDhqlZs2bq2rWrli5dqo0bNyogIEAbN250qM1JX9np3LmzFWQvWr16tUqWLKkXXnhBiYmJ2rZtm7Xst99+U3p6ujp37myNRUdHa8KECWrbtq1uueUWDRw4UD///LPDfr755hsFBATo1KlTmj17tjp37qwGDRooIyPD2mffvn11yy23KCgoKEdTEHJr7dq1uu+++9SsWTO1bt1a48aNc/iz9KXzPv/++28NGTJEt9xyi/r06aMNGzZk2V5GRoamT5+uDh06qFWrVnr++ed17tw59erVS6NHj5YknTp1SgEBAcrIyNAXX3xhvfePP/54lu3lZJ+59eCDD6pbt2763//+pxMnTljj2c013bRpkx544AHdeuut6tChg5588kkdOXIkR8dx6Wu3f/9+DRkyRE2bNtU333xz2f1dtHfvXg0ePFi33HKL+vfvr/Xr1zssj4iIUEBAgEJCQrKs2717d40ZMyZHPV6pj7lz56pPnz5q0qSJAgMDFRwcrHPnzlnLc/vZAAolA6DAq1+/vnnwwQeNMcbEx8eb0qVLm+DgYGv5+fPnTbly5czgwYOzrPvUU08Zd3d3ExMTY61/yy23mOrVq5svv/zSbN261XzyySfGy8vLjB071lrvvffeM5LMmDFjzHPPPWc2bNhgxo0bZ4wx5uzZs2bfvn1m37595q+//jJr1641w4cPN8WKFTPr16+3tnH48GFTvnx5... (line truncated to 2000 chars)
2966:       "text/plain": [
2967:        "<Figure size 800x500 with 1 Axes>"
2968:       ]
2969:      },
2970:      "metadata": {},
2971:      "output_type": "display_data"
2972:     }
2973:    ],
2974:    "source": [
2975:     "plt.figure(figsize=(8,5))\n",
2976:     "\n",
2977:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"avg_word_len\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
2978:     "\n",
2979:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"avg_word_len\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
2980:     "\n",
2981:     "plt.title(\"Average Word Length Distribution\")\n",
2982:     "plt.xlabel(\"Average Word Length\")\n",
2983:     "plt.legend()\n",
2984:     "\n",
2985:     "plt.show()"
2986:    ]
2987:   },
2988:   {
2989:    "cell_type": "code",
2990:    "execution_count": 287,
2991:    "id": "e5c984ac",
2992:    "metadata": {},
2993:    "outputs": [
2994:     {
2995:      "data": {
2996:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsnXd8HdWZsJ+Zub2o925Jtiz33js2mN4CgUASEkJIb5svZJPdJWzapiebtgkhhECoBgzYNOOCe++WZFWr93Z7mznfH1eWLUuyJVuSIbnPDyFr5rSZe+455z3nLZIQQhAhQoQIESJEiBAhQoQIV4B8tRsQIUKECBEiRIgQIUKEDz8RwSJChAgRIkSIECFChAhXTESwiBAhQoQIESJEiBAhwhUTESwiRIgQIUKECBEiRIhwxUQEiwgRIkSIECFChAgRIlwxEcEiQoQIESJEiBAhQoQIV0xEsIgQIUKECBEiRIgQIcIVExEsIkSIECFChAgRIkSIcMVEBIsIESJ8qFFVlXXr1lFSUjKi5TqdTtatW0dNTc2IljtURuu5Pmxc7c/harJhwwYOHTp0tZsRIUKECENGikTejhAhwqV466230Ol0rFmzps/1UCjE+vXrMZvN3Hjjjf3yvfLKKyQlJbFkyZJRa5vL5cJut/P973+f//iP/xhyvurqakpLSwkGg2RmZpKXl4fFYum9X1JSQmFhIU8//TT333//aDT9olzucw2HhoYGiouL8Xq9pKSkkJ2dTWJi4qjUdblczc/B7/fzxhtv9P4tSRJRUVFMmTKF1NTUUa8/JSWFm266ib/85S+jXleECBEijAS6q92ACBEifPD53e9+x9atW+ns7MRoNPZe37dvH3fddReSJNHa2kp8fHzvvdLSUu68807+7d/+bVQFi+GyadMmHnnkEU6fPs3cuXOx2WycPn2axsZG7r33Xn76058SGxt7tZs5qmzdupVHHnmEkydPMmvWLOLi4mhoaODIkSMsXLiQb37zm9x2221Xu5kAREVFceedd5KdnT3mdXd2dnLXXXeRl5fHjBkzEEJQVVXF0aNHufvuu3nyyScxm82jVv/NN9/M7NmzR638CBEiRBhpIqpQESJEuCSrVq3C6/Wyd+/ePte3bNlCRkYGBoOBrVu39rt3Nu8Hhaeeeoq1a9cyZ84cGhsb2bZtGxs2bKCsrIxXXnmFd955h+rq6qvdzFHlmWeeYfXq1cycOZOGhgZ27tzJ66+/zsGDB6mqqiI1NZW//e1vV7uZvaSlpbFu3TqWLl161dqwdu1a1q1bx8svv8zhw4f5wx/+wAsvvMBjjz02qvU+/vjjfO5znxvVOiJEiBBhJIkIFhEiRLgkZ4WDgYSHNWvWsGDBgl5B4ixbt25Fp9OxbNmyPtdPnTrFG2+8wbZt23C5XP3qeuONN3r1yuvr69m4cSOnTp3qvd/d3c0777zD1q1b8fv9Q36G+vp6Pve5z7F69Wr+/Oc/ExUV1ef+tddey86dO4ekChQIBNi9ezevv/46hw4dQlXVfnWtW7eOzs7OPteDwSDr1q3j9OnT/cq83OcaDvX19Tz00EOsXbuWP/3pT8TExPS5n5WVxUsvvcTXv/71fnmFEBw/fpw33niD7du34/P5+tzv6Ohg3bp1NDQ0AHD06FE2bNhAVVXVgO0Y6vsZyMZiOHUNtf3D4XOf+xw2m40NGzYMeL+6upo333yTd955h7a2tj731q9f309AP8uBAwdYv359798Xs7G4WB3vv/8+27Zt63Pt1KlTrFu3jjNnzvS5vnHjRg4ePNjnWk1NDe+99x5bt26lpaVlwPojRIgQYUBEhAgRIlwCTdNEfHy8WLp0ae81r9crjEaj+Pvf/y4effRRUVBQ0Cd9UlKSWLRoUe+1qqoqMW/ePGG328WqVatEQUGBsNvt4g9/+EOfuuLj48WDDz4oHnvsMTFlyhSxcOFC8R//8R9CCCGeffZZYbfb... (line truncated to 2000 chars)
2997:       "text/plain": [
2998:        "<Figure size 1000x500 with 1 Axes>"
2999:       ]
3000:      },
3001:      "metadata": {},
3002:      "output_type": "display_data"
3003:     }
3004:    ],
3005:    "source": [
3006:     "genuine_text = \" \".join(amazon_df[amazon_df[\"label\"] == 0][\"review\"])\n",
3007:     "\n",
3008:     "wordcloud = WordCloud(\n",
3009:     "    width=800,\n",
3010:     "    height=400,\n",
3011:     "    background_color=\"white\"\n",
3012:     ").generate(genuine_text)\n",
3013:     "\n",
3014:     "plt.figure(figsize=(10,5))\n",
3015:     "plt.imshow(wordcloud)\n",
3016:     "plt.axis(\"off\")\n",
3017:     "plt.title(\"Word Cloud - Genuine Reviews\")\n",
3018:     "plt.show()"
3019:    ]
3020:   },
3021:   {
3022:    "cell_type": "code",
3023:    "execution_count": 288,
3024:    "id": "8a4b1b2d",
3025:    "metadata": {},
3026:    "outputs": [
3027:     {
3028:      "data": {
3029:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXWcXeWd+P8+cl1G7rhPMnF3gRhJsOJWoLRAgVLf6rfd7v4KlOqWrewWKpQCLe4WLBCBEHfPZNx95rqe8/z+uJNLhpHMRCCw9/165QVz7jmPHH0+LgkhBEmSJEmSJEmSJEmSJElyCsif9ACSJEmSJEmSJEmSJEny6ScpWCRJkiRJkiRJkiRJkuSUSQoWSZIkSZIkSZIkSZIkOWWSgkWSJEmSJEmSJEmSJElOmaRgkSRJkiRJkiRJkiRJklMmKVgkSZIkSZIkSZIkSZLklEkKFkmSJEmSJEmSJEmSJDllkoJFkiRJkiRJkiRJkiRJTpmkYJEkSZKPFU3TeO655zh8+PBpbdfr9fLcc89RV1d3WtsdLmdqXknOfj4t1/61115jx44dn/QwkiRJ8hkmKVgkSfIZ5I033mD16tX9tsdiMZ577jlWrVo14HEvvPACGzZsOKNjCwaDXHvttTz33HMjOq62tpbVq1fz+uuvs2/fPgKBQJ/fGxsbufbaa3nvvfdO53CHzcnOayS8+OKLPPfcc0Sj0QF/D4fDPPfcc+zevXtE7TY1NfHuu+/y2muvsX37dtrb20/DaM8u3G43zz33HA0NDae97eFe+2PX59i/559/ntWrV9Pc3HzaxzQQt99+O3/+858/lr6SJEnyf5OkYJEkyWeQP/3pT1x++eWEw+E+27ds2cK1117LpZdeSmdnZ5/fysvLufrqq3nppZc+xpGemNWrVzNz5kwmTpzIL37xCx544AGuuuoqsrKyuOOOO+ju7v6kh/ixsGHDBq666iquvfZaXnnllQH36e7u5tprr+Xvf//7sNpcu3Ytc+fOpaysjLvuuou//e1vfPWrXyUnJ4dzzz33rLsXToXq6mquvfbaMy44D8Wx6/PjH/+Yp556iieeeIIf/ehH5Ofnc/311xMMBs9o/5deeimzZ88+o30kSZLk/zZJwSJJks8g5513HsFgkM2bN/fZvmbNGgoKCjAajaxdu7bfb8eOPVt49NFHufDCC5k9ezbNzc2sW7eO1157jaNHj/LCCy/w1ltvUVtb+0kP82Ph73//OwUFBUydOnXYgsNQPPbYY6xYsYIZM2bQ1NTEhg0beOWVV9i+fTvV1dXk5ubyyCOPnPrAk/TjwgsvTFgsdu7cyQMPPMDTTz/NPffcc0b7ffDBB/nqV796RvtIkiTJ/23UT3oASZIkOf0cEw7Wrl3LkiVLEtvXrFnDypUrqaqqYs2aNVxzzTWJ39auXYuqqixevLhPWwcOHKCqqgqHw8Hs2bOx2+19fn/11VfJy8tj1qxZNDY2snv3bkpKSpg0aRIQd0HZvHkzRqORhQsXDnsOjY2NfPWrX2XFihX87W9/6/f7+eefz4YNG1AU5YRtRSIRtm/fTkdHB/n5+UyfPr3PcY2NjWzatInly5eTlpaW2B6NRnn55ZeZMmUK48aN69Pmyc7rZHC73Tz77LP8+Mc/Jjs7m6997WvU1dVRVFR0Uu01NjZyxx13cOGFF/LXv/613+9FRUU8++yzrF+/vt9vQgj27dtHbW0tKSkpzJ07F7PZnPi9q6uLNWvWsHDhQvLy8ti9ezcNDQ1MmjSJ0tLSAccz0jb37NlDdXU1ixcvxuFw8PLLLyf2NZlMFBcXM2XKFCRJAuKuXu+88w4Qt9qpavzTN3HiRCZOnDjscRzjdF/7r371q/zwhz/ktdde49e//nW/32trazlw4ACKojBr1iwyMjISv7300kvk5OQwf/78fsdt27aNxsZGrrjiCiAeY5Gbm8usWbNG1Mf69esRQrB06dLEtgMH... (line truncated to 2000 chars)
3030:       "text/plain": [
3031:        "<Figure size 1000x500 with 1 Axes>"
3032:       ]
3033:      },
3034:      "metadata": {},
3035:      "output_type": "display_data"
3036:     }
3037:    ],
3038:    "source": [
3039:     "fake_text = \" \".join(amazon_df[amazon_df[\"label\"] == 1][\"review\"])\n",
3040:     "\n",
3041:     "wordcloud = WordCloud(\n",
3042:     "    width=800,\n",
3043:     "    height=400,\n",
3044:     "    background_color=\"white\"\n",
3045:     ").generate(fake_text)\n",
3046:     "\n",
3047:     "plt.figure(figsize=(10,5))\n",
3048:     "plt.imshow(wordcloud)\n",
3049:     "plt.axis(\"off\")\n",
3050:     "plt.title(\"Word Cloud - AI Generated Reviews\")\n",
3051:     "plt.show()"
3052:    ]
3053:   },
3054:   {
3055:    "cell_type": "code",
3056:    "execution_count": 289,
3057:    "id": "2b412c33",
3058:    "metadata": {},
3059:    "outputs": [
3060:     {
3061:      "data": {
3062:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXd8HdWduP1Mub2pd8kq7r03DLbBpkMAhxoIBELCLz2bbEh2NwvZZLObnrxpmyWETggYML0Y3AvuvVtW7/X2OnPeP658bVmSLcmS7WTvk4+C75mZc87MnZl7vl0SQgiSJEmSJEmSJEmSJEmS5DyQL/YEkiRJkiRJkiRJkiRJ8vdPUrBIkiRJkiRJkiRJkiTJeZMULJIkSZIkSZIkSZIkSXLeJAWLJEmSJEmSJEmSJEmSnDdJwSJJkiRJkiRJkiRJkiTnTVKwSJIkSZIkSZIkSZIkyXmTFCySJEmSJEmSJEmSJEly3iQFiyRJkiRJkiRJkiRJkpw3ScEiSZIkf9domsby5cs5fPjwkPbr9XpZvnw51dXVQ9pvfxmu8/p742J/DxeTt99+mx07dlzsaSRJkiRJv5GSlbeTJElyLt577z1UVWXp0qXd2mOxGCtWrMBisXDDDTf0OO61114jKyuLBQsWDNvcfD4fDoeDH/7wh/zbv/1bv4+rqqri6NGjRKNRCgsLKSsrw2q1JrYfPnyYcePG8dxzz3HvvfcOx9TPymDPayDU19dz6NAhgsEgOTk5jBgxgszMzGEZa7BczO8hHA7z1ltvJT5LkoTT6WTixInk5uYO+/g5OTnceOON/PnPfx72sZIkSZJkKFAv9gSSJEly6fO73/2O1atX09HRgclkSrRv2bKF22+/HUmSaGlpIT09PbHt6NGjLFu2jG9961vDKlgMlJUrV/Loo49y5MgRZs2ahd1u58iRIzQ0NHD33Xfz05/+lNTU1Is9zWFl9erVPProo+zfv5/p06eTlpZGfX09u3btYt68eXz729/mlltuudjTBMDpdLJs2TJGjBhxwcfu6Ojg9ttvp6ysjKlTpyKEoKKigt27d3PHHXfw1FNPYbFYhm38m266iRkzZgxb/0mSJEky1CRdoZIkSXJOrrzySoLBIJ988km39lWrVlFQUIDRaGT16tU9tp089lLhmWee4dprr2XmzJk0NDSwZs0a3n77bY4dO8Zrr73GBx98QFVV1cWe5rDy/PPPs2TJEqZNm0Z9fT0bNmzgzTffZPv27VRUVJCbm8vTTz99saeZIC8vj+XLl3P55ZdftDlce+21LF++nFdffZWdO3fyhz/8gb/97W/84Ac/GNZxn3jiCR555JFhHSNJkiRJhpKkYJEkSZJzclI46E14WLp0KXPnzk0IEidZvXo1qqpyxRVXdGs/cOAAb731FmvWrMHn8/UY66233kr4ldfV1fHOO+9w4MCBxHa3280HH3zA6tWrCYfD/T6Huro6HnnkEZYsWcL//u//4nQ6u22/+uqr2bBhQ79cgSKRCJs2beLNN99kx44daJrWY6zly5fT0dHRrT0ajbJ8+XKOHDnSo8/BntdAqKur4+GHH+baa6/lT3/6EykpKd22FxUV8corr/DNb36zx7FCCPbu3ctbb73FunXrCIVC3ba3t7ezfPly6uvrAdi9ezdvv/02FRUVvc6jv9entxiLgYzV3/kPhEceeQS73c7bb7/d6/aqqireffddPvjgA1pbW7ttW7FiRQ8B/STbtm1jxYoVic9ni7E42xhr165lzZo13doOHDjA8uXLqays7Nb+zjvvsH379m5t1dXVfPTRR6xevZrm5uZex0+SJEmSXhFJkiRJcg50XRfp6eni8ssvT7QFg0FhMpnEs88+Kx577DExZsyYbvtnZWWJ+fPnJ9oqKirE7NmzhcPhEFdeeaUYM2aMcDgc4g9/+EO3sdLT08VDDz0kfvCDH4iJEyeKefPmiX/7t38TQgjx4osv... (line truncated to 2000 chars)
3063:       "text/plain": [
3064:        "<Figure size 1000x500 with 1 Axes>"
3065:       ]
3066:      },
3067:      "metadata": {},
3068:      "output_type": "display_data"
3069:     }
3070:    ],
3071:    "source": [
3072:     "genuine_text = \" \".join(yelp_sample[yelp_sample[\"label\"] == 0][\"review\"])\n",
3073:     "\n",
3074:     "wordcloud = WordCloud(\n",
3075:     "    width=800,\n",
3076:     "    height=400,\n",
3077:     "    background_color=\"white\"\n",
3078:     ").generate(genuine_text)\n",
3079:     "\n",
3080:     "plt.figure(figsize=(10,5))\n",
3081:     "plt.imshow(wordcloud)\n",
3082:     "plt.axis(\"off\")\n",
3083:     "plt.title(\"Word Cloud - Genuine Reviews\")\n",
3084:     "plt.show()"
3085:    ]
3086:   },
3087:   {
3088:    "cell_type": "code",
3089:    "execution_count": 290,
3090:    "id": "8e53a10b",
3091:    "metadata": {},
3092:    "outputs": [
3093:     {
3094:      "data": {
3095:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXd4HdWZ+P+ZcnvRVe/Fkmy5924wBtu00GtISCABUjfZbMmSZfcXwqZvsimbhE1CSELomGITTDPYGIx777Ys2+q93d5mzu+PK137WpKtZhv43k8e8lhnZk6ZmXvmvOdtkhBCkCRJkiRJkiRJkiRJkiQjQL7YHUiSJEmSJEmSJEmSJMnHn6RgkSRJkiRJkiRJkiRJkhGTFCySJEmSJEmSJEmSJEkyYpKCRZIkSZIkSZIkSZIkSUZMUrBIkiRJkiRJkiRJkiTJiEkKFkmSJEmSJEmSJEmSJBkxScEiSZIkSZIkSZIkSZIkIyYpWCRJkiRJkiRJkiRJkmTEJAWLJEmSXFA0TePFF1/k8OHDo1qvx+PhxRdfpKamZlTrHSzna1xJPvp8XJ79a6+9xo4dOy52N5IkSfIJJilYJEnyCeSNN95gzZo1fcqj0Sgvvvgiq1ev7ve6l19+mQ0bNpzXvgUCAW6//XZefPHFIV1XXV3NmjVreP3119m3bx9+vz/heH19Pbfffjvvv//+aHZ30Ax3XEPhlVde4cUXXyQSifR7PBQK8eKLL7J79+4h1dvQ0MC7777La6+9xvbt22ltbR2F3n606O7u5sUXX6Surm7U6x7ss+99Pr3/vfTSS6xZs4bGxsZR71N/3H///fzf//3fBWkrSZIk/2+SFCySJPkE8tvf/pYbb7yRUCiUUL5lyxZuv/12rr/+etrb2xOOHT16lFtvvZWVK1dewJ6emzVr1jBz5kwmTpzID3/4Qx599FFuueUWsrKyeOCBB+js7LzYXbwgbNiwgVtuuYXbb7+dV199td9zOjs7uf322/nTn/40qDrXrVvH3LlzKS8v5+GHH+aPf/wjX/nKV8jJyeGSSy75yL0LI+HEiRPcfvvt511wPhu9z+c73/kOzz33HM888wwPPvgg+fn5fPrTnyYQCJzX9q+//npmz559XttIkiTJ/9skBYskST6BXHHFFQQCATZv3pxQvnbtWgoKCjAajaxbt67Psd5rPyo88cQTXH311cyePZvGxkbee+89XnvtNSorK3n55Zd56623qK6uvtjdvCD86U9/oqCggKlTpw5acDgbTz31FMuWLWPGjBk0NDSwYcMGXn31VbZv386JEyfIzc3lr3/968g7nqQPV199dVxjsXPnTh599FGef/55HnnkkfPa7mOPPcZXvvKV89pGkiRJ/t9GvdgdSJIkyejTKxysW7eOyy67LF6+du1ali9fzvHjx1m7di233XZb/Ni6detQVZXFixcn1HXgwAGOHz+Ow+Fg9uzZ2O32hON///vfycvLY9asWdTX17N7925KSkqYNGkSEDNB2bx5M0ajkYULFw56DPX19XzlK19h2bJl/PGPf+xz/Morr2TDhg0oinLOusLhMNu3b6etrY38/HymT5+ecF19fT2bNm1i6dKlpKamxssjkQirVq1iypQpVFRUJNQ53HENh+7ublasWMF3vvMdsrOz+epXv0pNTQ1FRUXDqq++vp4HHniAq6++mj/84Q99jhcVFbFixQrWr1/f55gQgn379lFdXU1KSgpz587FbDbHj3d0dLB27VoWLlxIXl4eu3fvpq6ujkmTJjFmzJh++zPUOvfs2cOJEydYvHgxDoeDVatWxc81mUwUFxczZcoUJEkCYqZe77zzDhDT2qlq7NM3ceJEJk6cOOh+9DLaz/4rX/kK3/72t3nttdf4yU9+0ud4dXU1Bw4cQFEUZs2aRUZGRvzYypUrycnJYf78+X2u27ZtG/X19dx0001AzMciNzeXWbNmDamN9evXI4Rg... (line truncated to 2000 chars)
3096:       "text/plain": [
3097:        "<Figure size 1000x500 with 1 Axes>"
3098:       ]
3099:      },
3100:      "metadata": {},
3101:      "output_type": "display_data"
3102:     }
3103:    ],
3104:    "source": [
3105:     "fake_text = \" \".join(yelp_sample[yelp_sample[\"label\"] == 1][\"review\"])\n",
3106:     "\n",
3107:     "wordcloud = WordCloud(\n",
3108:     "    width=800,\n",
3109:     "    height=400,\n",
3110:     "    background_color=\"white\"\n",
3111:     ").generate(fake_text)\n",
3112:     "\n",
3113:     "plt.figure(figsize=(10,5))\n",
3114:     "plt.imshow(wordcloud)\n",
3115:     "plt.axis(\"off\")\n",
3116:     "plt.title(\"Word Cloud - AI Generated Reviews\")\n",
3117:     "plt.show()"
3118:    ]
3119:   },
3120:   {
3121:    "cell_type": "code",
3122:    "execution_count": 291,
3123:    "id": "9e4c4ec4",
3124:    "metadata": {},
3125:    "outputs": [],
3126:    "source": [
3127:     "def plot_top_words(dataframe, label, title):\n",
3128:     "    vectorizer = CountVectorizer(stop_words=\"english\", max_features=20)\n",
3129:     "\n",
3130:     "    X = vectorizer.fit_transform(dataframe[dataframe[\"label\"] == label][\"review\"])\n",
3131:     "\n",
3132:     "    counts = np.asarray(X.sum(axis=0)).flatten()\n",
3133:     "\n",
3134:     "    words = vectorizer.get_feature_names_out()\n",
3135:     "\n",
3136:     "    pairs = sorted(zip(words, counts), key=lambda x: x[1], reverse=True)\n",
3137:     "\n",
3138:     "    words, counts = zip(*pairs)\n",
3139:     "\n",
3140:     "    plt.figure(figsize=(8,6))\n",
3141:     "    plt.barh(words, counts)\n",
3142:     "    plt.title(title)\n",
3143:     "    plt.xlabel(\"Frequency\")\n",
3144:     "    plt.gca().invert_yaxis()\n",
3145:     "    plt.show()"
3146:    ]
3147:   },
3148:   {
3149:    "cell_type": "code",
3150:    "execution_count": 292,
3151:    "id": "ae6776f1",
3152:    "metadata": {},
3153:    "outputs": [
3154:     {
3155:      "data": {
3156:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsYAAAIiCAYAAADLvQ4hAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAdHhJREFUeJzt3XdUVEfDBvCHpSxFutJkRQVF7LGBHSsaLCjGbixYYkk0MeYNxhJLgulqEhONXTFGjQK2WMGosceuqIAURQ0i7ALK0ub7g48bN6ABA+wCz++cPcc7d+7M3MXyZDJ3rp4QQoCIiIiIqIqTaXsARERERES6gMGYiIiIiAgMxkREREREABiMiYiIiIgAMBgTEREREQFgMCYiIiIiAsBgTEREREQEgMGYiIiIiAgAgzERUanLycnB6tWrcenSpf/cllKpxOrVqxEdHf3fB1aBVeXvYcuWLThx4oS2h0FUJejxzXdEFd/BgwcRHx//r/Xs7OzQr1+/Mh9PSkoKLl68iEePHsHFxQUtWrSAsbHxC+tHRUXh/PnzMDAwQPv27eHo6Pivffzyyy8wMDCAv7+/RnlWVhY2btwIU1NTDB8+vNB1a9euRc2aNeHj41PyGyum9PR0mJubY9GiRZgzZ85/aisyMhIeHh7YtGkTRo4cWUoj/JsQAjdv3sTNmzfx7NkzODg4oHbt2nBzcyv1vv6Lsv4eXubZs2cIDg6WjvX09GBhYYGmTZvC3d29zPt3cHBAnz59sHr16jLvi6iqM9D2AIjov7t16xYuX74sHcfFxeHw4cPo1KkT6tWrJ5W7urqWaTBOTU3FlClTsHPnTjRt2hRubm44d+4cMjMz8e2338LPz0+jfl5eHqZOnYr169ejd+/eePbsGUaOHIlPPvkEM2fOfGlfW7ZswYEDB/D666/DxMREKj916hQmTJgAAOjWrRvs7e2lc9evX0dAQAD+97//lWkwLk1WVlYICAgok6AaGhqKDz74AElJSWjXrh1sbGyQmJiI48ePo169eggMDMSIESNKvd9XUZbfw79RKpWYMGECGjZsiLZt20IIgbt37yIiIgI9e/bE9u3bYW5uXmb9jxgxAk2bNi2z9onoOYKIKp1du3YJAGLdunXl2u/NmzeFo6OjOHjwoFSWnZ0thgwZIgwMDMS1a9c06n/xxRdCJpOJY8eOSWWrV68WAMT+/ftf2tfSpUsFAHH48GGN8nnz5onatWsLU1NT8fPPP2uc+/bbbwUAceDAgVe9xWJJS0sTAMSiRYvKtJ//YsWKFQKAmDVrlnj69KnGucePH4uAgADh5+enpdHplgcPHggAYurUqRrlwcHBAoCYPn26dgZGRKWOa4yJqpDc3FycOHECmzZtQkhICJKSkgrV2bRpE06ePAkAuHz5MoKDgxEeHo7c3Nx/bd/W1hanT59Gjx49pDIDAwPMmjULOTk5+PXXX6XyvLw8fP311+jWrRs6deoklY8bNw4uLi744osvXtpX165dAQBHjx7VKD969Ch69OiBtm3bFnnOyMgIHTp0kMpyc3Nx8uRJ6Tv566+/CvW1efNmaY1nZGQkgoODceHCBen8gwcP8Msvv2DXrl1QqVQvHHNeXh5OnjyJn3/+GQcOHCjy+/+notbWJiUlYfXq1YiLi4MQAhEREdi8eXOx1zTHxsZi+vTp8Pf3x+eff64x4w7k/xxXr16Njz76qNC12dnZ+P3337Fp0yaEhYUhJSVF43xJxhYbG4vVq1fj8ePHGuVZWVlYvXo1rly5Uurfw7+NvySGDx8OCwsLHDhwoMjzly9fxpYtW/DLL78gNjZW49zGjRtx+PDhIq8LDw/Hhg0bpOOXrTF+WR/79u3D7t27NcrOnz+P1atX49atWxrlwcHBOH78uEbZtWvXsGPHDuzatatKru2mKkrLwZyIykBRM8bXr18X7u7uws7OTvj7+4vWrVsLuVwuPvvsM41rLS0txaRJk8Tk... (line truncated to 2000 chars)
3157:       "text/plain": [
3158:        "<Figure size 800x600 with 1 Axes>"
3159:       ]
3160:      },
3161:      "metadata": {},
3162:      "output_type": "display_data"
3163:     },
3164:     {
3165:      "data": {
3166:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAvYAAAIiCAYAAACjTowZAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAfYBJREFUeJzt3XdUVMfbB/AvS1kEKYJ0EEQExQJRY8UuKsHeayxYYmKsPxMxMUZjgqaYGGMSY4/R2BtqxIItiIrGrqCCFEUU266iLLDM+4cvN64UIYIru9/POXsOd+7cuc/cXeDZ2bmzBkIIASIiIiIiKtdk2g6AiIiIiIheHRN7IiIiIiIdwMSeiIiIiEgHMLEnIiIiItIBTOyJiIiIiHQAE3siIiIiIh3AxJ6IiIiISAcwsSciIiIi0gFM7ImItCwnJwdLlizBmTNnXrkthUKBJUuWID4+/tUDo3KlNF9HZWnNmjX4+++/tR0GkU4y4DfPEumfPXv2IDk5+aX17O3t0aVLlzKP58GDBzh9+jRu374Nd3d31KtXD6ampoXWv3btGk6ePAkjIyM0a9YMTk5OLz3HunXrYGRkhJ49e2qUZ2Vl4ffff4eZmRkGDBiQ77hly5bBxcUFHTp0KHnHiunx48ewsLDAF198gU8//fSV2oqNjUXNmjWxatUqDBo0qJQi/JcQAitWrIBarcbgwYMhl8vz1Xn69ClWr16NWrVqoUmTJsVu9/Lly7h8+TKePn0KR0dHeHh4wMvLq7S7oFX379/H5s2b0aZNG3h6epZq28V9HeU9P3kMDAxgaWmJunXrwsfHp1RjKoijoyM6deqEJUuWlPm5iPSNkbYDIKLXLy4uDmfPnpW2k5KSsG/fPrRo0QLVq1eXyqtVq1amif3Dhw/x/vvvY/Pmzahbty68vLwQExODzMxMLFiwAN26ddOon5ubiw8++AArVqxAUFAQnj59ikGDBuHLL7/E5MmTizzXmjVrEBERgXfeeQcVKlSQyqOjozFy5EgAQNu2beHg4CDtu3jxIkJCQvDxxx+XaWJfmqytrRESElJmCfGBAwcwfPhwAIC5uTn69++fr45CocDIkSPxwQcfFCux37ZtGz766COkp6ejadOmsLGxQWpqKo4cOYLq1asjNDQUAwcOLPW+aENycjJGjhyJP//8s9QT++LKe358fX3RpEkTCCFw/fp1HDx4EO3bt8eGDRtgYWFRZucfOHAg6tatW2btE+k1QUR6b8uWLQKAWL58+Ws97+XLl4WTk5PYs2ePVJadnS369u0rjIyMxIULFzTqf/PNN0Imk4lDhw5JZUuWLBEAxF9//VXkuX744QcBQOzbt0+j/LPPPhMeHh7CzMxM/Pnnnxr7FixYIACIiIiI/9rFYnn06JEAIL744osyPU9p6N+/v6hatap4++23RZs2bQqsc+vWLQFAfPDBBy9t7+effxYAxJQpU8STJ0809t29e1eEhISIbt26lUrsb4LTp08LAPlea6WhuK+jwp6f1atXCwBi/PjxpR4bEb0eHLEnokKp1WpER0fj+vXrsLCwQLNmzWBnZ6dRZ9WqVfD09ESzZs1w9uxZXLhwAc7OzmjRogUMDQ2LbN/W1hbHjh1DlSpVpDIjIyNMmTIF69atw6ZNm1CrVi0Az0br582bh7Zt26JFixZS/eHDh+OLL77AN998g44dOxZ6rjZt2gAAIiMj0bZtW6k8MjISgYGBSEhIQGRkJPr166exz8TEBAEBARrX5NixY0hISICFhQWaNm0Ke3t7jXP98ccf8PDwQEBAAGJjY3Hq1CnUqFED9evXBwDcunULhw8fhomJCdq2bQuZrODbnXJzcxEdHY3k5GTY2NigXr16+a7/ixQKBTZs2IDWrVujWrVqAID09HRs27YNgYGBqFKlCg4dOoQbN26gdu3a8Pf3L7K95+VNI5k5cyYcHBwwfPhwxMfHS+cpqcTERIwfPx49e/bE119/... (line truncated to 2000 chars)
3167:       "text/plain": [
3168:        "<Figure size 800x600 with 1 Axes>"
3169:       ]
3170:      },
3171:      "metadata": {},
3172:      "output_type": "display_data"
3173:     }
3174:    ],
3175:    "source": [
3176:     "plot_top_words(amazon_df, 0, \"Top 20 Words in Genuine Reviews\")\n",
3177:     "\n",
3178:     "plot_top_words(amazon_df, 1, \"Top 20 Words in AI Generated Reviews\")"
3179:    ]
3180:   },
3181:   {
3182:    "cell_type": "code",
3183:    "execution_count": 293,
3184:    "id": "bf66d309",
3185:    "metadata": {},
3186:    "outputs": [
3187:     {
3188:      "data": {
3189:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAtUAAAIiCAYAAAAHJDTKAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAfhtJREFUeJzt3XdYFNf7NvB7aYsgXRHQFZVmw4LdWECxICoqWGIwaqxRk/A10QRj1wQ1iSYmGhN7jyX23mussYKKooIYRQWBVaRz3j98mZ8rxcUFFpb7c117xTnzzJxnJogPhzNnZEIIASIiIiIiem962k6AiIiIiKi0Y1FNRERERKQhFtVERERERBpiUU1EREREpCEW1UREREREGmJRTURERESkIRbVREREREQaYlFNRERERKQhFtVERCVYRkYGlixZgitXrmh8rsTERCxZsgR3797VPLFSrCzfh3Xr1uHUqVPaToNIJ8n4RkUietOBAwfw4MGDd8bZ2tqie/fuRZ5PfHw8Ll++jCdPnsDR0REeHh4wNjbOMz4iIgIXL16EgYEBPvjgA9jb27+zjw0bNsDAwAD+/v4q7WlpaVi1ahVMTEzQv3//HMctW7YMlStXRqdOnQp+YWp6+fIlzMzMMGPGDEycOFGjc926dQu1atXC6tWrERgYWEgZ/h8hBG7evImbN28iOTkZdnZ2qFatGpydnQu9L00U9X3IT3JyMtauXStty2QymJubo169enBzcyvy/u3s7NC1a1csWbKkyPsiKmsMtJ0AEZUs4eHhuHr1qrQdFRWFQ4cOoU2bNnBxcZHanZycirSoTkhIwKhRo7BlyxbUq1cPzs7OuHDhAlJSUvDrr7+iR48eKvFZWVkYPXo0VqxYAR8fHyQnJyMwMBDfffcdvvzyy3z7WrduHfbv348uXbqgXLlyUvuZM2cwbNgwAED79u1RqVIlaV9YWBiGDBmCr7/+ukiL6sJkaWmJIUOGFEmRu337dowfPx7Pnj1Dy5YtYW1tjUePHuHkyZNwcXFBcHAwPvroo0Lv930U5X14l8TERAwbNgy1a9dGixYtIITA/fv3cezYMXTs2BGbNm2CmZlZkfX/0UcfoV69ekV2fqIyTRAR5WPr1q0CgFi+fHmx9nvz5k1hb28vDhw4ILWlp6eLvn37CgMDAxEaGqoS/8MPPwg9PT1x/PhxqW3JkiUCgNi7d2++ff38888CgDh06JBK++TJk0W1atWEiYmJWL9+vcq+X3/9VQAQ+/fvf99LVMuLFy8EADFjxowi7UcTCxcuFADEuHHjxKtXr1T2xcbGiiFDhogePXpoKbuS5fHjxwKAGD16tEr72rVrBQDxxRdfaCcxItIY51QT0XvJzMzEqVOnsHr1amzbtg3Pnj3LEbN69WqcPn0aAHD16lWsXbsWR48eRWZm5jvPb2Njg7Nnz6JDhw5Sm4GBAcaNG4eMjAz8/fffUntWVhbmzp2L9u3bo02bNlL7J598AkdHR/zwww/59tWuXTsAwJEjR1Tajxw5gg4dOqBFixa57jMyMkKrVq2ktszMTJw+fVq6J0+fPs3R15o1a6Q5rbdu3cLatWvx77//SvsfP36MDRs2YOvWrVAqlXnmnJWVhdOnT2P9+vXYv39/rvf/bbnNJX727BmWLFmCqKgoCCFw7NgxrFmzRu053JGRkfjiiy/g7++POXPmqIz0A6//Py5ZsgTffvttjmPT09Nx4sQJrF69Gjt27EB8fLzK/oLkFhkZiSVLliA2NlalPS0tDUuWLMG1a9cK/T68K/+C6N+/P8zNzbF///5c91+9ehXr1q3Dhg0bEBkZqbJv1apVOHToUK7HHT16FCtXrpS285tTnV8fe/bswc6dO1XaLl68iCVLliA8PFylfe3atTh58qRKW2hoKDZv3oytW7eWybnsVEZouagnohIut5HqsLAw4ebmJmxtbYW/v79o0qSJkMvlYvbs2SrHWlhYiBEj... (line truncated to 2000 chars)
3190:       "text/plain": [
3191:        "<Figure size 800x600 with 1 Axes>"
3192:       ]
3193:      },
3194:      "metadata": {},
3195:      "output_type": "display_data"
3196:     },
3197:     {
3198:      "data": {
3199:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAtYAAAIiCAYAAADsE4/JAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAgTlJREFUeJzs3XdUFNfbB/AvdZG2gFIUEEREUVBEImJFxajBhlhji7HFxCTG5KchGo2aBE2i0WiqvWBssffesbeIiIIFFDGiworCAst9//Awb1aKS1xYWL6fc/Yc584zd54ZV3283LljIIQQICIiIiKi12Ko6wSIiIiIiPQBC2siIiIiIi1gYU1EREREpAUsrImIiIiItICFNRERERGRFrCwJiIiIiLSAhbWRERERERawMKaiIiIiEgLWFgTEWlRbm4uFi5ciIsXL752X+np6Vi4cCESEhJePzGqULT5PSpNq1atwrFjx3SdBlG5YcA3LxJVbHv27EFiYuIr4xwcHNCtW7dSz+fJkye4cOECHjx4ADc3N/j7+8PMzKzI+Pj4eJw9exbGxsZo0aIFqlev/spzrFmzBsbGxggPD1drz87OxvLly2Fubo633367wHGLFy+Gs7MzOnbsWPIL01BGRgasrKwwffp0TJo06bX6unbtGry9vbFixQoMHDhQSxn+PyEEli5dCpVKhUGDBkEmkxWIyczMRFRUFBo0aICgoCCN+42NjUVsbCwyMzPh5OQEd3d3eHp6avsSdOrx48fYsGED2rVrBw8PD632ren3KP/3J5+BgQGsra3RsGFD1K1bV6s5FcbJyQldunTBwoULS/1cRBWBsa4TIKLXExcXh0uXLknbd+7cwb59+9C6dWvUqVNHaq9du3apFtZpaWl4//33sWHDBjRs2BCenp44c+YMsrKyMG/ePPTo0UMtPi8vDx988AGWLl2Kzp07IzMzEwMHDsQ333yDTz/9tNhzrVq1Crt378Zbb72FKlWqSO3R0dEYMWIEAKB9+/ZwdHSU9sXExGDYsGGYMGFCqRbW2mRjY4Nhw4aVWkF68OBBvPvuuwAACwsL9O/fv0BMeno6RowYgQ8++ECjwnrz5s0YP348Hj58iObNm8POzg7Jyck4evQo6tSpg4iICAwYMEDr16ILiYmJGDFiBP7880+tF9aayv/9qV+/PoKCgiCEwK1bt3Do0CG8+eabWLduHaysrErt/AMGDEDDhg1LrX+iCkcQkV7ZuHGjACCWLFlSpueNjY0V1atXF3v27JHacnJyRN++fYWxsbG4cuWKWvz3338vDA0NxeHDh6W2hQsXCgBi586dxZ5rzpw5AoDYt2+fWvvkyZOFu7u7MDc3F3/++afavnnz5gkAYvfu3f/1EjXy9OlTAUBMnz69VM+jDf379xe1atUSb7zxhmjXrl2hMffv3xcAxAcffPDK/n755RcBQPzvf/8Tz58/V9uXmpoqhg0bJnr06KGV3MuDCxcuCAAFvmvaoOn3qKjfn6ioKAFAfPzxx1rPjYiKxhFrokpCpVIhOjoat27dgpWVFVq0aAF7e3u1mBUrVsDDwwMtWrTApUuXcOXKFdSoUQOtW7eGkZFRsf1XrVoVJ0+eRM2aNaU2Y2Nj/O9//8OaNWvw119/oUGDBgBejFbPnj0b7du3R+vWraX4d999F9OnT8f333+PTp06FXmudu3aAQAOHDiA9u3bS+0HDhxAhw4dcPPmTRw4cAD9+vVT22dqaoqWLVuq3ZOTJ0/i5s2bsLKyQvPmzeHg4KB2rpUrV8Ld3R0tW7bEtWvXcO7cOdSrVw9NmjQBANy/fx9HjhyBqakp2rdvD0PDwh9dycvLQ3R0NBITE2FnZwd/f/8C9/9l6enpWLduHdq2bYvatWsDAB4+fIjNmzejQ4cOqFmzJg4fPoy7d+/Cx8cHfn5+xfb3b/nTGKZOnQpHR0e8++67SEhIkM5TUrdv38bHH3+M8PBwfPfd... (line truncated to 2000 chars)
3200:       "text/plain": [
3201:        "<Figure size 800x600 with 1 Axes>"
3202:       ]
3203:      },
3204:      "metadata": {},
3205:      "output_type": "display_data"
3206:     }
3207:    ],
3208:    "source": [
3209:     "plot_top_words(yelp_sample, 0, \"Top 20 Words in Genuine Reviews\")\n",
3210:     "\n",
3211:     "plot_top_words(yelp_sample, 1, \"Top 20 Words in AI Generated Reviews\")"
3212:    ]
3213:   },
3214:   {
3215:    "cell_type": "code",
3216:    "execution_count": 294,
3217:    "id": "ac76aa3f",
3218:    "metadata": {},
3219:    "outputs": [
3220:     {
3221:      "data": {
3222:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAA3IAAAIOCAYAAAD9QD/vAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAtDhJREFUeJzs3XdYVEf7N/AvdZGOUqQLKqAidkUjCgo2LFhjN/YYu9Ek2Dtq9JHYu7F3Y4kdBXvHLmABBASlygLC0vb9w5fzc6mLGnHl+7muvZ6cOXNm7jngc+3NzJmjJJVKpSAiIiIiIiKFoVzWARAREREREVHpMJEjIiIiIiJSMEzkiIiIiIiIFAwTOSIiIiIiIgXDRI6IiIiIiEjBMJEjIiIiIiJSMEzkiIiIiIiIFAwTOSIiIiIiIgXDRI6IiL6KVatWQV9fH8nJyWUdSpko7+Mvzw4fPgx9fX08evSorEMp0v3796Gvr48TJ06UdShEJCcmckRECuT8+fPQ19eX63P//v3/NJYdO3bI9GdgYICqVauibdu2OHLkSIH6GRkZSE5OhlQq/U/j+lb91+PP+3nUrl27yD7y6pw/f16uNmNiYjBjxgw0bdoUFhYWsLS0hLOzMwYPHgw/Pz/k5uZ+ySGUqaVLl0JfXx9paWlfvO3MzEwkJycjJyen2Hr5/00ZGhrCwcEBw4cPR1hY2BeP62PZ2dlITk5GVlbWf9oPEX05TOSIiBRIy5YtER4eLvPR0tKCjY1NgfLatWv/p7FIJBIkJydj8+bNCA8PR1hYGE6ePIlq1aqha9euWLlypUz9sWPHIikpCXp6ev9pXN+q/3r869atg7q6Oh4/flxkopb3M5Pny/qJEyfg4OCAgIAA/P7777h27Rpu3bqFhQsXIisrC23atMHff//9hUdRdr6FPzTk/zf15MkTLFu2DKdPn4azszNiY2P/s77r1auHpKQkeHp6/md9ENGXxUSOiEiBqKqqFph5U1JSgoqKSoFyFRWVrxKTlpaW0Ke9vT1WrVoFU1NTbN68WaaeSCQS4i2P/svxBwUF4dq1a/jf//6H6tWrY+PGjZ/V3tOnT9GzZ0+0atUKAQEB8PLygpWVFUxNTdGqVSvs3LkTJ06cgKam5hcaAX0s79+UiYkJPD09sWjRIsTGxmLbtm3/WZ95/x+ipqb2n/VBRF8WEzkiou/Q48eP0bt3b1hbWwtfvo8ePSpTZ8GCBdDX18f79+8xefJk2NjYwNraGiNHjkRCQsIn962kpASRSFQgkSzqGbGrV6+idevWqFy5MurXr4/9+/cX+kxRXrzp6emYOnUq7OzsUK1aNQDA/v37ZZZ4WlhYoH379jhz5kyhY05PT8dvv/0GW1tbVK9eHcuXLwfwYUZkypQpqFq1KqytrTF16tQCywcTEhIwadIk1K5dG6ampmjatCmWLFmCjIyMYu9LYePPi0cikWDmzJmoWrUqLC0tMXTo0FI9S7dx40YYGRmhV69e+Pnnn3HkyBHEx8fLfX1+8+bNQ2ZmJlasWFHkHwTat2+P3r17y5RFR0dj7NixcHBwgLGxMRo2bIg1a9bIzHKVdsylafNTfzfGjRuHBQsWAAAsLCwKXZ4sTxwAcP36dbi7u8v8Pn+umjVrAgDCw8NlyiUSCXx8fNCgQQOYmJjA3t4eU6ZMQUpKilDfwMAAS5YsKdBmYmIijI2NMX36dABFPyNXUh/Z2dmwsLDAjBkzZK6rVasW9PX1ERQUJJTlLQ2/evUqACA3NxfLly9H48aNYWZmhjp16mDMmDGIiYn5jLtFVH4wkSMi+s7cvXsXTZo0QXx8PA4fPoxLly6hQYMG8PLyklnumJ6ejuTkZIwfPx729va4ePEi1q9fj1OnTqF169YlJiaFkUgkWLZsGcLDwzFkyBCZc4UtXbt27RpatWoFAwMDnD17Frt378aFCxdw6NChAs8UfRyvtbU1zpw5g19++QUA0LVrV2FJ... (line truncated to 2000 chars)
3223:       "text/plain": [
3224:        "<Figure size 900x600 with 1 Axes>"
3225:       ]
3226:      },
3227:      "metadata": {},
3228:      "output_type": "display_data"
3229:     }
3230:    ],
3231:    "source": [
3232:     "vectorizer = CountVectorizer(\n",
3233:     "    stop_words=\"english\",\n",
3234:     "    ngram_range=(2,2),\n",
3235:     "    max_features=20\n",
3236:     ")\n",
3237:     "\n",
3238:     "X = vectorizer.fit_transform(amazon_df[amazon_df[\"label\"] == 1][\"review\"])\n",
3239:     "\n",
3240:     "counts = np.asarray(X.sum(axis=0)).flatten()\n",
3241:     "\n",
3242:     "bigrams = vectorizer.get_feature_names_out()\n",
3243:     "\n",
3244:     "pairs = sorted(zip(bigrams, counts), key=lambda x: x[1], reverse=True)\n",
3245:     "\n",
3246:     "bigrams, counts = zip(*pairs)\n",
3247:     "\n",
3248:     "plt.figure(figsize=(9,6))\n",
3249:     "plt.barh(bigrams, counts)\n",
3250:     "plt.title(\"Top Bigrams in AI Generated Reviews\")\n",
3251:     "plt.gca().invert_yaxis()\n",
3252:     "plt.show()"
3253:    ]
3254:   },
3255:   {
3256:    "cell_type": "code",
3257:    "execution_count": 295,
3258:    "id": "f37d5337",
3259:    "metadata": {},
3260:    "outputs": [
3261:     {
3262:      "data": {
3263:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAA1wAAAIOCAYAAACs1AyMAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAp0NJREFUeJzs3XdYVFfbLvB7hjL0IiIoIiAiiij2brBgQUFsiQ1jL7HEGpVEXzUaNRqNicYWC1Gx944FsRc0dmwICCogKDIUGdo+f3jYnyMDDMYRhft3XVzn3Ws/e61nb/A782StvUYiCIIAIiIiIiIi+uikxZ0AERERERFRScWCi4iIiIiISENYcBEREREREWkICy4iIiIiIiINYcFFRERERESkISy4iIiIiIiINIQFFxERERERkYaw4CIiIiIiItIQFlxERJSHp6cnvLy8ijuNYlPa7780Gzx4MGrVqlXcaRTol19+gZmZWXGnQURqYsFFRKQhEyZMgJmZWaE/NWrU0HguvXr1UhrTwsICrq6uGDhwIEJDQ/PEJycnIyUlReN5fa40ff+5v48pU6YUGGNtba12n5cvX8bgwYPh6uoKKysrODk5oVWrVvjpp5/w8OHDj5H2Z6NVq1bo0qWLRvpOTU2FXC4vNO79f1NWVlZo0KAB5s6di/T0dI3kluvNmzdISkrS6BhE9PGw4CIi0pBffvkFkZGR4s/evXuRlJSE0aNHK7VfvHhR47mkpKQgPT1dHPPBgwdYvXo1QkND0aBBA9y/f18p/ujRozh48KDG8/pcafL+Y2JisGvXLujq6mLt2rVQKBQq41JSUvD69Wu1+pw0aRKaNm0KXV1drFq1Cjdv3sSxY8cwdOhQHD16FM7Oznj58uVHvIvi9Tn8B4H3/01dvnwZvXv3xrRp09CrVy+Njj1t2jQkJiZqdAwi+ni0izsBIqKSSl9fH/r6+uKxkZERAEBPT6/YlgO9O27ZsmXx559/onHjxti6dStmzpwpnsvNtbTS5P2vX78e2tra2LFjB1q2bIndu3ejd+/eH9zf77//jkWLFmHt2rUYNGiQ0jkHBwf07NkTfn5+/zVtykfuvykzMzNMmDABFy9exM6dO/Ho0SM4OTlpZEw9PT3o6elppG8i+vg4w0VEVMy2bdsGd3d3WFtbw97eHr6+vnmWgDVt2hS9evXC48eP4ePjgwoVKqBmzZpYsmQJBEH44LFzP7RpaWkptef3DtPSpUtRq1YtlC9fHp06dcK9e/dUvvOSm29ERAS+/vprVKxYEd9//z0AoH///kpLG52cnDBo0CA8efJEZR/h4eHo0qULKlSogCZNmuDcuXMAgLCwMHTt2hU2NjZwc3PD3r178+R79epVdO/eHVWqVEGlSpXQoUMHHDp0qNDnour+c/N5+vQpvv76a1SoUAEuLi74448/Cu0vlyAIWLduHb755hu4u7ujRYsWWLNmjdrXvy89PR2zZ89GgwYN8hRbubS0tLBgwQJYWFgotZ87dw5dunRBpUqVUL58eXh6euL8+fNKMUW956L0+aF/G46Ojrhx4wZOnz6d77JcdfIAgOXLl8PNzU3p7/m/cnFxAQBERkYqtUdGRmLYsGFwcnJCuXLl0LhxY6xfv14pFzMzM9y9ezdPn1u3boWZmZk4G57fO1yFjXHy5EmYmZnh0qVLYtv169dhZmaGunXrKvU1YcIEVK5cWfy/LzExMRg1ahRq1KiBChUqoFmzZvjzzz+RmZlZtAdEVBoJRET0SYSEhAgAhNmzZ4ttc+fOFSQSiTBt2jQhLCxMuHz5stC8eXPBxMREuHPnjhhXo0YN4auvvhI8PDyEoKAgISIiQli8eLGgra0tTJ48udCxO3XqJMhkMqW2mJgYwdvbWzA0NBTu37+vdK5Zs2aCu7u7Utu0adMELS0tYcGCBUJERIRw7tw5oV27doKHh4dgZ2enFJubb9u2bYWTJ08KDx48EPz9/QVB... (line truncated to 2000 chars)
3264:       "text/plain": [
3265:        "<Figure size 900x600 with 1 Axes>"
3266:       ]
3267:      },
3268:      "metadata": {},
3269:      "output_type": "display_data"
3270:     }
3271:    ],
3272:    "source": [
3273:     "vectorizer = CountVectorizer(\n",
3274:     "    stop_words=\"english\",\n",
3275:     "    ngram_range=(2,2),\n",
3276:     "    max_features=20\n",
3277:     ")\n",
3278:     "\n",
3279:     "X = vectorizer.fit_transform(yelp_sample[yelp_sample[\"label\"] == 1][\"review\"])\n",
3280:     "\n",
3281:     "counts = np.asarray(X.sum(axis=0)).flatten()\n",
3282:     "\n",
3283:     "bigrams = vectorizer.get_feature_names_out()\n",
3284:     "\n",
3285:     "pairs = sorted(zip(bigrams, counts), key=lambda x: x[1], reverse=True)\n",
3286:     "\n",
3287:     "bigrams, counts = zip(*pairs)\n",

(Output capped at 50 KB. Showing lines 2674-3287. Use offset=3288 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 4.2s)

_Thinking:_

Let me continue reading the rest of the notebook to understand the full structure before making a plan.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 3288
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
3288:     "\n",
3289:     "plt.figure(figsize=(9,6))\n",
3290:     "plt.barh(bigrams, counts)\n",
3291:     "plt.title(\"Top Bigrams in AI Generated Reviews\")\n",
3292:     "plt.gca().invert_yaxis()\n",
3293:     "plt.show()"
3294:    ]
3295:   },
3296:   {
3297:    "cell_type": "code",
3298:    "execution_count": 296,
3299:    "id": "a728bb12",
3300:    "metadata": {},
3301:    "outputs": [
3302:     {
3303:      "data": {
3304:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArMAAAJOCAYAAACk64/cAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAi+JJREFUeJzs3XdYFFfbBvB7FxAsNBVEELGgIqixYxdErNiNYI0t9p7E2GsMscYeTew91thrFHvvXUQRFOxSlbZ7vj98mS8rxUUXdhbu33XN9b5z5syZZzYqD8+eOaMQQggQERERERkgpb4DICIiIiL6UkxmiYiIiMhgMZklIiIiIoPFZJaIiIiIDBaTWSIiIiIyWExmiYiIiMhgMZklIiIiIoPFZJaIiIiIDBaTWSIiIiIyWExmiYhSMWrUKBgbGxvMuIaOnwsRfSkms0SUJdRqNTZs2IAmTZrA1tYWpqamKFq0KBo0aIBly5YhNjZW3yHqzLBhw2BmZqbvMFL47bffoFAooFAocP78+VT7VKxYEQqFAs7Ozl90DbneOxFlX0xmiSjTxcXFoXnz5ujTpw88PT1x/vx5REdH49SpU2jatClGjBiBBQsW6DvMLPHbb78hKSlJrzHkzZsXq1atStF+9epVXL9+HXnz5s3ymOTwuRCRYWIyS0SZbujQoTh06BD27t2Ln3/+GcWLF0euXLlQtGhR/PTTT7h8+TKKFCmi7zBzjLZt22LTpk2Ii4vTaF+5ciWcnZ1RsWJF/QRGRPQFmMwSUaZ6+vQpli9fjnbt2qF+/fqp9ilVqhS6dOki7atUKkyfPh0uLi4wNTVFwYIF4evri4cPH2qcZ2VlhX79+uHs2bOoXbs2cufOjUmTJuHUqVNQKBTYs2cP/vjjDzg7O8PIyAiXLl0CANy+fRvffvstbGxsYGpqirJly2L+/PmfvZe5c+dKX9MrFApYWFigfv362L9/v9SndevWmDdvHuLj4zX6BgcHA0h7bujRo0fh6ekJc3Nz5MmTB+7u7ti+fbtGn379+sHKygoxMTHo2bMnrKysYGVlha5duyIqKuqz8Sfr1q0boqKisHPnTqktISEBGzZsQPfu3TPt3pPjj4iIQPfu3ZE/f36ULVs21c/lzZs3KFq0KKpUqaKRdD9//hz29vaoWbMmEhMTtb5nIsq+mMwSUaY6cuQIVCoVmjZtqvU5PXr0wKRJkzBy5Ei8ePECR48eRXBwMNzd3fH48WONvo8fP4a/vz/++usvBAYGonLlytKxFStW4NmzZzh58iQCAgKQO3duXLhwAdWrV0diYiJOnDiB169fY+rUqRg/fjxGjRqVblzDhg2DEAJCCKhUKty8eROVKlVCq1atcOXKFQDAP//8g6FDh8LU1FTqK4RAsWLF0hx39+7d8Pb2hpOTE27duoWgoCDUr18f7dq1w9KlS1P0Hzx4MNq3b4/Q0FD8/fff2LlzJ0aOHKn151ukSBE0bNhQY6rBrl278O7dO3Tr1i3T771fv35o3749goKC0oy7QIEC2LJlC27evInBgwcD+PhLjp+fHxITE7F582aYmJhofc9ElI0JIqJMNGnSJAFAHDlyRKv+V65cEQDEhAkTNNqfPn0qTE1NxXfffSe1WVpairx584o3b95o9D158qQAILy9vVOMX61aNVGqVCkRHx+v0T5r1ixhbGwswsLChBBC/Pzzz8LIyEirmIsVKyYGDRok7Q8dOlSYmpqm2je1cUuXLi1cXFyESqXSaPfy8hJWVlbi/fv3Qggh+vbtKwCIzZs3a/QbPHiwyJUrl0hMTEw3Tn9/fwFA3L17V2zYsEEYGRmJZ8+eCSGEaNasmfR51a5dW5QsWVKLO8/YvSfHv3r16hTH0vq858+fLwCIlStXipEjRwqlUikOHjyoVWxElDOwMktEsvLvv/8C+Div878cHBxQo0YN6XiyOnXqIH/+/KmO1bJlS439Fy9e4OLFi2jVqhVy... (line truncated to 2000 chars)
3305:       "text/plain": [
3306:        "<Figure size 800x600 with 2 Axes>"
3307:       ]
3308:      },
3309:      "metadata": {},
3310:      "output_type": "display_data"
3311:     }
3312:    ],
3313:    "source": [
3314:     "feature_cols = [\n",
3315:     "    \"text_length\",\n",
3316:     "    \"word_count\",\n",
3317:     "    \"sentence_count\",\n",
3318:     "    \"avg_word_len\",\n",
3319:     "    \"vocab_richness\",\n",
3320:     "    \"label\"\n",
3321:     "]\n",
3322:     "\n",
3323:     "corr = amazon_df[feature_cols].corr()\n",
3324:     "\n",
3325:     "plt.figure(figsize=(8,6))\n",
3326:     "plt.imshow(corr)\n",
3327:     "\n",
3328:     "plt.colorbar()\n",
3329:     "\n",
3330:     "plt.xticks(range(len(feature_cols)), feature_cols, rotation=45)\n",
3331:     "\n",
3332:     "plt.yticks(range(len(feature_cols)), feature_cols)\n",
3333:     "\n",
3334:     "plt.title(\"Correlation Matrix\")\n",
3335:     "\n",
3336:     "plt.tight_layout()\n",
3337:     "plt.show()"
3338:    ]
3339:   },
3340:   {
3341:    "cell_type": "code",
3342:    "execution_count": 297,
3343:    "id": "73665682",
3344:    "metadata": {},
3345:    "outputs": [
3346:     {
3347:      "data": {
3348:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArMAAAJOCAYAAACk64/cAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAi95JREFUeJzs3XdYFFfbBvB7KYIiRQFFqiIiYokdFY2gYu8Ne9QYNZZYkhh7T4gxGnuJLXaNLRq7RrHE3k1EBBRFwIJKVdru+f7wZb6sFBdd2Fm4f9c115s5c+bMM/uKPD575oxCCCFARERERKSHDHQdABERERHRh2IyS0RERER6i8ksEREREektJrNEREREpLeYzBIRERGR3mIyS0RERER6i8ksEREREektJrNEREREpLeYzBIRERGR3mIyS0SUhfHjx8PIyEhvxtV3/FyI6EMxmSWifKFSqbBlyxa0bNkSpUqVgomJCZydndGkSROsXr0aSUlJug5Ra0aPHg1TU1Ndh5HJjz/+CIVCAYVCgYsXL2bZp3r16lAoFHBzc/uga8j13omo4GIyS0R5Ljk5GW3atMHgwYPh6+uLixcvIiEhAWfPnkWrVq0wduxYLF68WNdh5osff/wR6enpOo3BzMwMv/32W6b269ev4+bNmzAzM8v3mOTwuRCRfmIyS0R5btSoUTh69CgOHDiA7777DuXKlUORIkXg7OyMb7/9FlevXoWjo6Ouwyw0OnfujG3btiE5OVmtfd26dXBzc0P16tV1ExgR0QdgMktEeerx48dYs2YNunTpgsaNG2fZp0KFCujTp4+0r1QqMWfOHHh4eMDExAQ2Njbw9/dHaGio2nlWVlYYOnQozp8/D29vbxQtWhTTp0/H2bNnoVAosH//fixfvhxubm4wNDTElStXAAD//vsvunXrBltbW5iYmKBSpUpYtGjRe+9lwYIF0tf0CoUCFhYWaNy4MQ4dOiT16dixIxYuXIiUlBS1vuHh4QCynxt64sQJ+Pr6wtzcHMWKFYOXlxd2796t1mfo0KGwsrJCYmIiBg4cCCsrK1hZWaFv376Ij49/b/wZ+vXrh/j4eOzdu1dqS01NxZYtW9C/f/88u/eM+GNjY9G/f3+ULFkSlSpVyvJzefHiBZydnVGrVi21pPvJkyewt7dH/fr1kZaWpvE9E1HBxWSWiPLU8ePHoVQq0apVK43PGTBgAKZPn45x48bh6dOnOHHiBMLDw+Hl5YUHDx6o9X3w4AECAgKwatUqhISEoGbNmtKxtWvXIjIyEmfOnEFgYCCKFi2KS5cuoW7dukhLS8Pp06cRExODWbNmYcqUKRg/fnyOcY0ePRpCCAghoFQqcfv2bdSoUQMdOnTAtWvXAAB//PEHRo0aBRMTE6mvEAJly5bNdtw///wTfn5+cHFxwT///IOwsDA0btwYXbp0wcqVKzP1HzlyJLp27YqIiAhs374de/fuxbhx4zT+fB0dHdGsWTO1qQb79u3Dq1ev0K9fvzy/96FDh6Jr164ICwvLNm5ra2vs2LEDt2/fxsiRIwG8/UdOjx49kJaWht9//x3GxsYa3zMRFWCCiCgPTZ8+XQAQx48f16j/tWvXBAAxdepUtfbHjx8LExMT8dlnn0ltlpaWwszMTLx48UKt75kzZwQA4efnl2n8OnXqiAoVKoiUlBS19p9//lkYGRmJqKgoIYQQ3333nTA0NNQo5rJly4oRI0ZI+6NGjRImJiZZ9s1qXHd3d+Hh4SGUSqVae9OmTYWVlZV4/fq1EEKIIUOGCADi999/V+s3cuRIUaRIEZGWlpZjnAEBAQKACAoKElu2bBGGhoYiMjJSCCFE69atpc/L29tblC9fXoM7z929Z8S/fv36TMey+7wXLVokAIh169aJcePGCQMDA3HkyBGNYiOiwoGVWSKSlb/++gvA23md/+Xg4IB69epJxzM0bNgQJUuWzHKs9u3bq+0/ffoUly9fRocO... (line truncated to 2000 chars)
3349:       "text/plain": [
3350:        "<Figure size 800x600 with 2 Axes>"
3351:       ]
3352:      },
3353:      "metadata": {},
3354:      "output_type": "display_data"
3355:     }
3356:    ],
3357:    "source": [
3358:     "feature_cols = [\n",
3359:     "    \"text_length\",\n",
3360:     "    \"word_count\",\n",
3361:     "    \"sentence_count\",\n",
3362:     "    \"avg_word_len\",\n",
3363:     "    \"vocab_richness\",\n",
3364:     "    \"label\"\n",
3365:     "]\n",
3366:     "\n",
3367:     "corr = yelp_sample[feature_cols].corr()\n",
3368:     "\n",
3369:     "plt.figure(figsize=(8,6))\n",
3370:     "plt.imshow(corr)\n",
3371:     "\n",
3372:     "plt.colorbar()\n",
3373:     "\n",
3374:     "plt.xticks(range(len(feature_cols)), feature_cols, rotation=45)\n",
3375:     "\n",
3376:     "plt.yticks(range(len(feature_cols)), feature_cols)\n",
3377:     "\n",
3378:     "plt.title(\"Correlation Matrix\")\n",
3379:     "\n",
3380:     "plt.tight_layout()\n",
3381:     "plt.show()"
3382:    ]
3383:   },
3384:   {
3385:    "cell_type": "code",
3386:    "execution_count": 298,
3387:    "id": "ad75625e",
3388:    "metadata": {},
3389:    "outputs": [
3390:     {
3391:      "data": {
3392:       "text/html": [
3393:        "<div>\n",
3394:        "<style scoped>\n",
3395:        "    .dataframe tbody tr th:only-of-type {\n",
3396:        "        vertical-align: middle;\n",
3397:        "    }\n",
3398:        "\n",
3399:        "    .dataframe tbody tr th {\n",
3400:        "        vertical-align: top;\n",
3401:        "    }\n",
3402:        "\n",
3403:        "    .dataframe thead tr th {\n",
3404:        "        text-align: left;\n",
3405:        "    }\n",
3406:        "\n",
3407:        "    .dataframe thead tr:last-of-type th {\n",
3408:        "        text-align: right;\n",
3409:        "    }\n",
3410:        "</style>\n",
3411:        "<table border=\"1\" class=\"dataframe\">\n",
3412:        "  <thead>\n",
3413:        "    <tr>\n",
3414:        "      <th></th>\n",
3415:        "      <th colspan=\"8\" halign=\"left\">text_length</th>\n",
3416:        "      <th colspan=\"8\" halign=\"left\">word_count</th>\n",
3417:        "      <th colspan=\"8\" halign=\"left\">sentence_count</th>\n",
3418:        "      <th colspan=\"8\" halign=\"left\">avg_word_len</th>\n",
3419:        "      <th colspan=\"8\" halign=\"left\">vocab_richness</th>\n",
3420:        "    </tr>\n",
3421:        "    <tr>\n",
3422:        "      <th></th>\n",
3423:        "      <th>count</th>\n",
3424:        "      <th>mean</th>\n",
3425:        "      <th>std</th>\n",
3426:        "      <th>min</th>\n",
3427:        "      <th>25%</th>\n",
3428:        "      <th>50%</th>\n",
3429:        "      <th>75%</th>\n",
3430:        "      <th>max</th>\n",
3431:        "      <th>count</th>\n",
3432:        "      <th>mean</th>\n",
3433:        "      <th>std</th>\n",
3434:        "      <th>min</th>\n",
3435:        "      <th>25%</th>\n",
3436:        "      <th>50%</th>\n",
3437:        "      <th>75%</th>\n",
3438:        "      <th>max</th>\n",
3439:        "      <th>count</th>\n",
3440:        "      <th>mean</th>\n",
3441:        "      <th>std</th>\n",
3442:        "      <th>min</th>\n",
3443:        "      <th>25%</th>\n",
3444:        "      <th>50%</th>\n",
3445:        "      <th>75%</th>\n",
3446:        "      <th>max</th>\n",
3447:        "      <th>count</th>\n",
3448:        "      <th>mean</th>\n",
3449:        "      <th>std</th>\n",
3450:        "      <th>min</th>\n",
3451:        "      <th>25%</th>\n",
3452:        "      <th>50%</th>\n",
3453:        "      <th>75%</th>\n",
3454:        "      <th>max</th>\n",
3455:        "      <th>count</th>\n",
3456:        "      <th>mean</th>\n",
3457:        "      <th>std</th>\n",
3458:        "      <th>min</th>\n",
3459:        "      <th>25%</th>\n",
3460:        "      <th>50%</th>\n",
3461:        "      <th>75%</th>\n",
3462:        "      <th>max</th>\n",
3463:        "    </tr>\n",
3464:        "    <tr>\n",
3465:        "      <th>label</th>\n",
3466:        "      <th></th>\n",
3467:        "      <th></th>\n",
3468:        "      <th></th>\n",
3469:        "      <th></th>\n",
3470:        "      <th></th>\n",
3471:        "      <th></th>\n",
3472:        "      <th></th>\n",
3473:        "      <th></th>\n",
3474:        "      <th></th>\n",
3475:        "      <th></th>\n",
3476:        "      <th></th>\n",
3477:        "      <th></th>\n",
3478:        "      <th></th>\n",
3479:        "      <th></th>\n",
3480:        "      <th></th>\n",
3481:        "      <th></th>\n",
3482:        "      <th></th>\n",
3483:        "      <th></th>\n",
3484:        "      <th></th>\n",
3485:        "      <th></th>\n",
3486:        "      <th></th>\n",
3487:        "      <th></th>\n",
3488:        "      <th></th>\n",
3489:        "      <th></th>\n",
3490:        "      <th></th>\n",
3491:        "      <th></th>\n",
3492:        "      <th></th>\n",
3493:        "      <th></th>\n",
3494:        "      <th></th>\n",
3495:        "      <th></th>\n",
3496:        "      <th></th>\n",
3497:        "      <th></th>\n",
3498:        "      <th></th>\n",
3499:        "      <th></th>\n",
3500:        "      <th></th>\n",
3501:        "      <th></th>\n",
3502:        "      <th></th>\n",
3503:        "      <th></th>\n",
3504:        "      <th></th>\n",
3505:        "      <th></th>\n",
3506:        "    </tr>\n",
3507:        "  </thead>\n",
3508:        "  <tbody>\n",
3509:        "    <tr>\n",
3510:        "      <th>0</th>\n",
3511:        "      <td>20215.0</td>\n",
3512:        "      <td>383.558348</td>\n",
3513:        "      <td>402.202223</td>\n",
3514:        "      <td>24.0</td>\n",
3515:        "      <td>117.0</td>\n",
3516:        "      <td>217.0</td>\n",
3517:        "      <td>484.0</td>\n",
3518:        "      <td>2095.0</td>\n",
3519:        "      <td>20215.0</td>\n",
3520:        "      <td>75.199159</td>\n",
3521:        "      <td>77.811015</td>\n",
3522:        "      <td>5.0</td>\n",
3523:        "      <td>23.0</td>\n",
3524:        "      <td>43.0</td>\n",
3525:        "      <td>95.0</td>\n",
3526:        "      <td>381.0</td>\n",
3527:        "      <td>20215.0</td>\n",
3528:        "      <td>1.0</td>\n",
3529:        "      <td>0.0</td>\n",
3530:        "      <td>1.0</td>\n",
3531:        "      <td>1.0</td>\n",
3532:        "      <td>1.0</td>\n",
3533:        "      <td>1.0</td>\n",
3534:        "      <td>1.0</td>\n",
3535:        "      <td>20215.0</td>\n",
3536:        "      <td>4.109831</td>\n",
3537:        "      <td>0.436404</td>\n",
3538:        "      <td>2.545455</td>\n",
3539:        "      <td>3.827659</td>\n",
3540:        "      <td>4.074074</td>\n",
3541:        "      <td>4.352941</td>\n",
3542:        "      <td>7.300000</td>\n",
3543:        "      <td>20215.0</td>\n",
3544:        "      <td>0.803361</td>\n",
3545:        "      <td>0.133560</td>\n",
3546:        "      <td>0.317073</td>\n",
3547:        "      <td>0.704545</td>\n",
3548:        "      <td>0.815789</td>\n",
3549:        "      <td>0.909091</td>\n",
3550:        "      <td>1.0</td>\n",
3551:        "    </tr>\n",
3552:        "    <tr>\n",
3553:        "      <th>1</th>\n",
3554:        "      <td>20192.0</td>\n",
3555:        "      <td>296.262827</td>\n",
3556:        "      <td>298.076633</td>\n",
3557:        "      <td>37.0</td>\n",
3558:        "      <td>93.0</td>\n",
3559:        "      <td>169.0</td>\n",
3560:        "      <td>370.0</td>\n",
3561:        "      <td>1665.0</td>\n",
3562:        "      <td>20192.0</td>\n",
3563:        "      <td>63.140055</td>\n",
3564:        "      <td>63.753927</td>\n",
3565:        "      <td>7.0</td>\n",
3566:        "      <td>19.0</td>\n",
3567:        "      <td>36.0</td>\n",
3568:        "      <td>79.0</td>\n",
3569:        "      <td>322.0</td>\n",
3570:        "      <td>20192.0</td>\n",
3571:        "      <td>1.0</td>\n",
3572:        "      <td>0.0</td>\n",
3573:        "      <td>1.0</td>\n",
3574:        "      <td>1.0</td>\n",
3575:        "      <td>1.0</td>\n",
3576:        "      <td>1.0</td>\n",
3577:        "      <td>1.0</td>\n",
3578:        "      <td>20192.0</td>\n",
3579:        "      <td>3.765257</td>\n",
3580:        "      <td>0.419527</td>\n",
3581:        "      <td>1.666667</td>\n",
3582:        "      <td>3.488372</td>\n",
3583:        "      <td>3.714286</td>\n",
3584:        "      <td>3.977549</td>\n",
3585:        "      <td>7.636364</td>\n",
3586:        "      <td>20192.0</td>\n",
3587:        "      <td>0.721480</td>\n",
3588:        "      <td>0.182635</td>\n",
3589:        "      <td>0.029412</td>\n",
3590:        "      <td>0.593750</td>\n",
3591:        "      <td>0.750000</td>\n",
3592:        "      <td>0.869565</td>\n",
3593:        "      <td>1.0</td>\n",
3594:        "    </tr>\n",
3595:        "  </tbody>\n",
3596:        "</table>\n",
3597:        "</div>"
3598:       ],
3599:       "text/plain": [
3600:        "      text_length                                                             \\\n",
3601:        "            count        mean         std   min    25%    50%    75%     max   \n",
3602:        "label                                                                          \n",
3603:        "0         20215.0  383.558348  402.202223  24.0  117.0  217.0  484.0  2095.0   \n",
3604:        "1         20192.0  296.262827  298.076633  37.0   93.0  169.0  370.0  1665.0   \n",
3605:        "\n",
3606:        "      word_count                                                      \\\n",
3607:        "           count       mean        std  min   25%   50%   75%    max   \n",
3608:        "label                                                                  \n",
3609:        "0        20215.0  75.199159  77.811015  5.0  23.0  43.0  95.0  381.0   \n",
3610:        "1        20192.0  63.140055  63.753927  7.0  19.0  36.0  79.0  322.0   \n",
3611:        "\n",
3612:        "      sentence_count                                    avg_word_len  \\\n",
3613:        "               count mean  std  min  25%  50%  75%  max        count   \n",
3614:        "label                                                                  \n",
3615:        "0            20215.0  1.0  0.0  1.0  1.0  1.0  1.0  1.0      20215.0   \n",
3616:        "1            20192.0  1.0  0.0  1.0  1.0  1.0  1.0  1.0      20192.0   \n",
3617:        "\n",
3618:        "                                                                             \\\n",
3619:        "           mean       std       min       25%       50%       75%       max   \n",
3620:        "label                                                                         \n",
3621:        "0      4.109831  0.436404  2.545455  3.827659  4.074074  4.352941  7.300000   \n",
3622:        "1      3.765257  0.419527  1.666667  3.488372  3.714286  3.977549  7.636364   \n",
3623:        "\n",
3624:        "      vocab_richness                                                    \\\n",
3625:        "               count      mean       std       min       25%       50%   \n",
3626:        "label                                                                    \n",
3627:        "0            20215.0  0.803361  0.133560  0.317073  0.704545  0.815789   \n",
3628:        "1            20192.0  0.721480  0.182635  0.029412  0.593750  0.750000   \n",
3629:        "\n",
3630:        "                      \n",
3631:        "            75%  max  \n",
3632:        "label                 \n",
3633:        "0      0.909091  1.0  \n",
3634:        "1      0.869565  1.0  "
3635:       ]
3636:      },
3637:      "execution_count": 298,
3638:      "metadata": {},
3639:      "output_type": "execute_result"
3640:     }
3641:    ],
3642:    "source": [
3643:     "summary = amazon_df.groupby(\"label\")[\n",
3644:     "    [\n",
3645:     "        \"text_length\",\n",
3646:     "        \"word_count\",\n",
3647:     "        \"sentence_count\",\n",
3648:     "        \"avg_word_len\",\n",
3649:     "        \"vocab_richness\"\n",
3650:     "    ]\n",
3651:     "].describe()\n",
3652:     "\n",
3653:     "summary"
3654:    ]
3655:   },
3656:   {
3657:    "cell_type": "code",
3658:    "execution_count": 299,
3659:    "id": "6cf166cb",
3660:    "metadata": {},
3661:    "outputs": [
3662:     {
3663:      "data": {
3664:       "text/html": [
3665:        "<div>\n",
3666:        "<style scoped>\n",
3667:        "    .dataframe tbody tr th:only-of-type {\n",
3668:        "        vertical-align: middle;\n",
3669:        "    }\n",
3670:        "\n",
3671:        "    .dataframe tbody tr th {\n",
3672:        "        vertical-align: top;\n",
3673:        "    }\n",
3674:        "\n",
3675:        "    .dataframe thead tr th {\n",
3676:        "        text-align: left;\n",
3677:        "    }\n",
3678:        "\n",
3679:        "    .dataframe thead tr:last-of-type th {\n",
3680:        "        text-align: right;\n",
3681:        "    }\n",
3682:        "</style>\n",
3683:        "<table border=\"1\" class=\"dataframe\">\n",
3684:        "  <thead>\n",
3685:        "    <tr>\n",
3686:        "      <th></th>\n",
3687:        "      <th colspan=\"8\" halign=\"left\">text_length</th>\n",
3688:        "      <th colspan=\"8\" halign=\"left\">word_count</th>\n",
3689:        "      <th colspan=\"8\" halign=\"left\">sentence_count</th>\n",
3690:        "      <th colspan=\"8\" halign=\"left\">avg_word_len</th>\n",
3691:        "      <th colspan=\"8\" halign=\"left\">vocab_richness</th>\n",
3692:        "    </tr>\n",
3693:        "    <tr>\n",
3694:        "      <th></th>\n",
3695:        "      <th>count</th>\n",
3696:        "      <th>mean</th>\n",
3697:        "      <th>std</th>\n",
3698:        "      <th>min</th>\n",
3699:        "      <th>25%</th>\n",
3700:        "      <th>50%</th>\n",
3701:        "      <th>75%</th>\n",
3702:        "      <th>max</th>\n",
3703:        "      <th>count</th>\n",
3704:        "      <th>mean</th>\n",
3705:        "      <th>std</th>\n",
3706:        "      <th>min</th>\n",
3707:        "      <th>25%</th>\n",
3708:        "      <th>50%</th>\n",
3709:        "      <th>75%</th>\n",
3710:        "      <th>max</th>\n",
3711:        "      <th>count</th>\n",
3712:        "      <th>mean</th>\n",
3713:        "      <th>std</th>\n",
3714:        "      <th>min</th>\n",
3715:        "      <th>25%</th>\n",
3716:        "      <th>50%</th>\n",
3717:        "      <th>75%</th>\n",
3718:        "      <th>max</th>\n",
3719:        "      <th>count</th>\n",
3720:        "      <th>mean</th>\n",
3721:        "      <th>std</th>\n",
3722:        "      <th>min</th>\n",
3723:        "      <th>25%</th>\n",
3724:        "      <th>50%</th>\n",
3725:        "      <th>75%</th>\n",
3726:        "      <th>max</th>\n",
3727:        "      <th>count</th>\n",
3728:        "      <th>mean</th>\n",
3729:        "      <th>std</th>\n",
3730:        "      <th>min</th>\n",
3731:        "      <th>25%</th>\n",
3732:        "      <th>50%</th>\n",
3733:        "      <th>75%</th>\n",
3734:        "      <th>max</th>\n",
3735:        "    </tr>\n",
3736:        "    <tr>\n",
3737:        "      <th>label</th>\n",
3738:        "      <th></th>\n",
3739:        "      <th></th>\n",
3740:        "      <th></th>\n",
3741:        "      <th></th>\n",
3742:        "      <th></th>\n",
3743:        "      <th></th>\n",
3744:        "      <th></th>\n",
3745:        "      <th></th>\n",
3746:        "      <th></th>\n",
3747:        "      <th></th>\n",
3748:        "      <th></th>\n",
3749:        "      <th></th>\n",
3750:        "      <th></th>\n",
3751:        "      <th></th>\n",
3752:        "      <th></th>\n",
3753:        "      <th></th>\n",
3754:        "      <th></th>\n",
3755:        "      <th></th>\n",
3756:        "      <th></th>\n",
3757:        "      <th></th>\n",
3758:        "      <th></th>\n",
3759:        "      <th></th>\n",
3760:        "      <th></th>\n",
3761:        "      <th></th>\n",
3762:        "      <th></th>\n",
3763:        "      <th></th>\n",
3764:        "      <th></th>\n",
3765:        "      <th></th>\n",
3766:        "      <th></th>\n",
3767:        "      <th></th>\n",
3768:        "      <th></th>\n",
3769:        "      <th></th>\n",
3770:        "      <th></th>\n",
3771:        "      <th></th>\n",
3772:        "      <th></th>\n",
3773:        "      <th></th>\n",
3774:        "      <th></th>\n",
3775:        "      <th></th>\n",
3776:        "      <th></th>\n",
3777:        "      <th></th>\n",
3778:        "    </tr>\n",
3779:        "  </thead>\n",
3780:        "  <tbody>\n",
3781:        "    <tr>\n",
3782:        "      <th>0</th>\n",
3783:        "      <td>24883.0</td>\n",
3784:        "      <td>634.296267</td>\n",
3785:        "      <td>563.243612</td>\n",
3786:        "      <td>20.0</td>\n",
3787:        "      <td>255.0</td>\n",
3788:        "      <td>474.0</td>\n",
3789:        "      <td>831.0</td>\n",
3790:        "      <td>4848.0</td>\n",
3791:        "      <td>24883.0</td>\n",
3792:        "      <td>123.018165</td>\n",
3793:        "      <td>108.85437</td>\n",
3794:        "      <td>2.0</td>\n",
3795:        "      <td>49.0</td>\n",
3796:        "      <td>92.0</td>\n",
3797:        "      <td>162.0</td>\n",
3798:        "      <td>964.0</td>\n",
3799:        "      <td>24883.0</td>\n",
3800:        "      <td>1.0</td>\n",
3801:        "      <td>0.0</td>\n",
3802:        "      <td>1.0</td>\n",
3803:        "      <td>1.0</td>\n",
3804:        "      <td>1.0</td>\n",
3805:        "      <td>1.0</td>\n",
3806:        "      <td>1.0</td>\n",
3807:        "      <td>24883.0</td>\n",
3808:        "      <td>4.213053</td>\n",
3809:        "      <td>0.396267</td>\n",
3810:        "      <td>2.375000</td>\n",
3811:        "      <td>3.975475</td>\n",
3812:        "      <td>4.166667</td>\n",
3813:        "      <td>4.391304</td>\n",
3814:        "      <td>9.500000</td>\n",
3815:        "      <td>24883.0</td>\n",
3816:        "      <td>0.744078</td>\n",
3817:        "      <td>0.122175</td>\n",
3818:        "      <td>0.365488</td>\n",
3819:        "      <td>0.65625</td>\n",
3820:        "      <td>0.738318</td>\n",
3821:        "      <td>0.828348</td>\n",
3822:        "      <td>1.0</td>\n",
3823:        "    </tr>\n",
3824:        "    <tr>\n",
3825:        "      <th>1</th>\n",
3826:        "      <td>24547.0</td>\n",
3827:        "      <td>436.217705</td>\n",
3828:        "      <td>444.094634</td>\n",
3829:        "      <td>20.0</td>\n",
3830:        "      <td>157.0</td>\n",
3831:        "      <td>306.0</td>\n",
3832:        "      <td>559.0</td>\n",
3833:        "      <td>4907.0</td>\n",
3834:        "      <td>24547.0</td>\n",
3835:        "      <td>84.416996</td>\n",
3836:        "      <td>86.13125</td>\n",
3837:        "      <td>2.0</td>\n",
3838:        "      <td>30.0</td>\n",
3839:        "      <td>59.0</td>\n",
3840:        "      <td>108.0</td>\n",
3841:        "      <td>976.0</td>\n",
3842:        "      <td>24547.0</td>\n",
3843:        "      <td>1.0</td>\n",
3844:        "      <td>0.0</td>\n",
3845:        "      <td>1.0</td>\n",
3846:        "      <td>1.0</td>\n",
3847:        "      <td>1.0</td>\n",
3848:        "      <td>1.0</td>\n",
3849:        "      <td>1.0</td>\n",
3850:        "      <td>24547.0</td>\n",
3851:        "      <td>4.254301</td>\n",
3852:        "      <td>0.515841</td>\n",
3853:        "      <td>2.142857</td>\n",
3854:        "      <td>3.965517</td>\n",
3855:        "      <td>4.192308</td>\n",
3856:        "      <td>4.461538</td>\n",
3857:        "      <td>30.666667</td>\n",
3858:        "      <td>24547.0</td>\n",
3859:        "      <td>0.790980</td>\n",
3860:        "      <td>0.124140</td>\n",
3861:        "      <td>0.301546</td>\n",
3862:        "      <td>0.70339</td>\n",
3863:        "      <td>0.789474</td>\n",
3864:        "      <td>0.882353</td>\n",
3865:        "      <td>1.0</td>\n",
3866:        "    </tr>\n",
3867:        "  </tbody>\n",
3868:        "</table>\n",
3869:        "</div>"
3870:       ],
3871:       "text/plain": [
3872:        "      text_length                                                             \\\n",
3873:        "            count        mean         std   min    25%    50%    75%     max   \n",
3874:        "label                                                                          \n",
3875:        "0         24883.0  634.296267  563.243612  20.0  255.0  474.0  831.0  4848.0   \n",
3876:        "1         24547.0  436.217705  444.094634  20.0  157.0  306.0  559.0  4907.0   \n",
3877:        "\n",
3878:        "      word_count                                                        \\\n",
3879:        "           count        mean        std  min   25%   50%    75%    max   \n",
3880:        "label                                                                    \n",
3881:        "0        24883.0  123.018165  108.85437  2.0  49.0  92.0  162.0  964.0   \n",
3882:        "1        24547.0   84.416996   86.13125  2.0  30.0  59.0  108.0  976.0   \n",
3883:        "\n",
3884:        "      sentence_count                                    avg_word_len  \\\n",
3885:        "               count mean  std  min  25%  50%  75%  max        count   \n",
3886:        "label                                                                  \n",
3887:        "0            24883.0  1.0  0.0  1.0  1.0  1.0  1.0  1.0      24883.0   \n",
3888:        "1            24547.0  1.0  0.0  1.0  1.0  1.0  1.0  1.0      24547.0   \n",
3889:        "\n",
3890:        "                                                                              \\\n",
3891:        "           mean       std       min       25%       50%       75%        max   \n",
3892:        "label                                                                          \n",
3893:        "0      4.213053  0.396267  2.375000  3.975475  4.166667  4.391304   9.500000   \n",
3894:        "1      4.254301  0.515841  2.142857  3.965517  4.192308  4.461538  30.666667   \n",
3895:        "\n",
3896:        "      vocab_richness                                                   \\\n",
3897:        "               count      mean       std       min      25%       50%   \n",
3898:        "label                                                                   \n",
3899:        "0            24883.0  0.744078  0.122175  0.365488  0.65625  0.738318   \n",
3900:        "1            24547.0  0.790980  0.124140  0.301546  0.70339  0.789474   \n",
3901:        "\n",
3902:        "                      \n",
3903:        "            75%  max  \n",
3904:        "label                 \n",
3905:        "0      0.828348  1.0  \n",
3906:        "1      0.882353  1.0  "
3907:       ]
3908:      },
3909:      "execution_count": 299,
3910:      "metadata": {},
3911:      "output_type": "execute_result"
3912:     }
3913:    ],
3914:    "source": [
3915:     "summary = yelp_sample.groupby(\"label\")[\n",
3916:     "    [\n",
3917:     "        \"text_length\",\n",
3918:     "        \"word_count\",\n",
3919:     "        \"sentence_count\",\n",
3920:     "        \"avg_word_len\",\n",
3921:     "        \"vocab_richness\"\n",
3922:     "    ]\n",
3923:     "].describe()\n",
3924:     "\n",
3925:     "summary"
3926:    ]
3927:   },
3928:   {
3929:    "cell_type": "code",
3930:    "execution_count": null,
3931:    "id": "2156475f",
3932:    "metadata": {},
3933:    "outputs": [],
3934:    "source": []
3935:   }
3936:  ],
3937:  "metadata": {
3938:   "kernelspec": {
3939:    "display_name": "work (3.12.3.final.0)",
3940:    "language": "python",
3941:    "name": "python3"
3942:   },
3943:   "language_info": {
3944:    "codemirror_mode": {
3945:     "name": "ipython",
3946:     "version": 3
3947:    },
3948:    "file_extension": ".py",
3949:    "mimetype": "text/x-python",
3950:    "name": "python",
3951:    "nbconvert_exporter": "python",
3952:    "pygments_lexer": "ipython3",
3953:    "version": "3.12.3"
3954:   }
3955:  },
3956:  "nbformat": 4,
3957:  "nbformat_minor": 5
3958: }

(End of file - total 3958 lines)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 19.3s)

_Thinking:_

Now I have a complete understanding of the notebook. Let me analyze its structure and create a plan for adding comments and markdown cells to make it more understandable.

The notebook is about **Cross-Domain Fake Review Detection** using Amazon and Yelp datasets. Here's the flow:

1. **Data Loading & Initial Exploration**
   - Load Amazon and Yelp datasets
   - Display basic info (shape, columns, missing values)
   - Preview data with head()

2. **Label Mapping & Column Standardization**
   - Map Amazon labels: CG→1, OR→0
   - Map Yelp labels: -1→1, 1→0
   - Rename columns to match between datasets
   - Drop unnecessary columns (keep only rating, review, label)

3. **Data Cleaning**
   - Remove duplicates based on review text
   - Define a `count_patterns` function to find HTML tags, URLs, emails
   - Define a `clean_review` function that:
     - Decodes HTML entities
     - Removes HTML tags, URLs, emails
     - Removes encoding artifacts
     - Removes special characters
     - Lowercases text
   - Apply cleaning to both datasets
   - Remove empty reviews
   - Filter reviews with < 20 characters   - Check class balance

4. **EDA (Exploratory Data Analysis)**
   - Class distribution plots
   - Feature engineering: text_length, word_count, sentence_count
   - Vocabulary richness calculation
   - Average word length calculation
   - Distribution plots for all features
   - Word clouds for genuine vs AI-generated reviews
   - Top words and bigrams analysis
   - Correlation matrix
   - Summary statistics by label

Now let me plan the documentation. I'll add:
1. A title markdown cell at the top
2. Section headers (markdown cells) before each major step
3. Brief comments in code cells where needed
4. A conclusion/summary section

Let me create the plan.

Now I have a full understanding of the notebook. Here's my plan:

---

## Plan: Document `cross-domain-V2.ipynb`

The notebook is a **Cross-Domain Fake Review Detection** pipeline that processes Amazon and Yelp review datasets, cleans them, performs EDA, and engineers features. It currently has almost no markdown cells or meaningful comments.

### What I'll add:

**Markdown cells (section headers + brief descriptions):**

1. **Top of notebook** - Title + brief project description
2. Before label mapping for Amazon - "Label Mapping"
3. Before column renaming/standardization - "Column Standardization"
4. Before duplicate removal - "Duplicate Removal"
5. Before `count_patterns` / `clean_review` - "Text Cleaning"
6. Before empty/short review filtering - "Review Length Filtering"
7. Before class balance check - "Class Balance Check"
8. The existing "### EDA" cell is fine, but I'll expand it slightly
9. Before feature engineering cells - "Feature Engineering"
10. Before distribution plots - "Distribution Analysis"
11. Before word clouds - "Word Cloud Visualization"
12. Before top words/bigrams - "N-Gram Analysis"
13. Before correlation matrix - "Correlation Analysis"
14. Before summary statistics - "Summary Statistics"

**Inline code comments** - Only add where the code is non-obvious (e.g., the `clean_review` regex steps, label mapping conventions). I won't over-comment obvious code like `amazon_df.head()`.

### Style:
- Brief, not heavy - each markdown cell will be 1-2 lines max
- No emojis
- Keep existing code comments, just enhance where needed

### Files to modify:
- `cross-domain-V2.ipynb` - insert ~14 new markdown cells and a handful of inline comments

---

Want me to proceed with this plan?

---

## User

dont add the comments and markdown instead help me add those tell me what should i do and then ill say how i want it to be done 

---

## Assistant (Plan · MiMo V2.5 Free · 25.4s)

_Thinking:_

The user wants me to tell them what comments and markdown they should add to their notebook, rather than me adding them directly. They want to decide how they want it done. Let me provide a clear plan of what markdown cells and comments to add, organized by the notebook flow.

Got it. Here's what I'd recommend adding to `cross-domain-V2.ipynb`:

---

## 1. Title Cell (new markdown at top)
Something like: `# Cross-Domain Fake Review Detection` with a one-liner about what the notebook does (load Amazon + Yelp reviews, clean, EDA, feature engineering for detecting fake/AI-generated reviews).

---

## 2. Before `amazon_df.head()` / `yelp_df.head()` (cells 3-4)
No markdown needed - already self-explanatory.

---

## 3. Before the label mapping cell (cell 7, line 461)
A markdown cell like: `### Label Encoding` — explains you're converting string labels (`CG`/`OR` for Amazon, `-1`/`1` for Yelp) into a unified binary format: `1 = fake/AI-generated`, `0 = genuine`.

---

## 4. Before column renaming/selection (cells 8-9, lines 562-680)
A markdown cell like: `### Column Standardization` — rename and keep only `rating`, `review`, `label` so both datasets share the same schema.

---

## 5. Before duplicate removal (cells 11-14, lines 883-943)
A markdown cell like: `### Duplicate Removal` — drop duplicate reviews based on the review text.

---

## 6. Before `count_patterns` and `clean_review` (cells 15-18, lines 950-1067)
A markdown cell like: `### Text Cleaning` — brief list of what gets cleaned (HTML tags, URLs, emails, encoding artifacts, special chars, lowercasing).

Also add a short comment inside `clean_review` before each regex step explaining *what* it removes (you already have some, but they could be a touch more specific).

---

## 7. Before empty/short review filtering (cells 19-22, lines 1083-1098)
A markdown cell like: `### Remove Empty & Short Reviews` — drop rows with empty or very short reviews (under 20 chars) since they don't carry useful signal.

---

## 8. Before class balance check (cells 23-24, lines 1132-1171)
A markdown cell like: `### Class Distribution` — check if genuine vs fake reviews are balanced. If Yelp is imbalanced, note that you'll sample to balance it.

---

## 9. Before Yelp sampling (cell 25, line 1191)
A markdown cell like: `### Balance Yelp Dataset` — randomly sample 25k from each class to create a balanced subset, since the original Yelp data is heavily skewed (~90% genuine).

---

## 10. Before the `### EDA` markdown (cell 28, line 2035)
Expand it slightly to: `### Exploratory Data Analysis` — one line about what EDA covers (distributions, word clouds, n-grams, correlations).

---

## 11. Before feature engineering cells (cells 33-34, lines 2480-2600)
A markdown cell like: `### Feature Engineering` — list the features being created: `text_length`, `word_count`, `sentence_count`, `vocab_richness`, `avg_word_len`.

---

## 12. Before distribution/histogram plots (cells 35-40, lines 2619-2986)
A markdown cell like: `### Feature Distributions` — comparing genuine vs fake reviews across all engineered features (word count, sentence count, vocab richness, avg word length).

---

## 13. Before word clouds (cells 41-44, lines 3005-3118)
A markdown cell like: `### Word Clouds` — visualizing most frequent words in genuine vs AI-generated reviews for each dataset.

---

## 14. Before top words / bigrams (cells 45-48, lines 3126-3294)
A markdown cell like: `### N-Gram Analysis` — top 20 unigrams and bigrams in fake reviews to spot common patterns.

---

## 15. Before correlation matrix (cells 49-50, lines 3313-3382)
A markdown cell like: `### Correlation Analysis` — heatmap showing how features relate to each other and to the label.

---

## 16. Before summary stats (cells 51-52, lines 3642-3926)
A markdown cell like: `### Summary Statistics by Class` — descriptive stats grouped by label to quantify differences between genuine and fake reviews.

---

That's **~14 new markdown cells** total. Want me to adjust any of these, or do you want to change the wording/level of detail on any of them?

---

## User

before cell 41 i want to explain what im checking by review length i will tell you my thinking which you can format and frame it well like before 
"since we are checking for computer generated or ai generated review here i would like to remove reviews which are shorter than a specific length since it would be very hard to tell wheather it is ai or not and regardless of that fact ai text is tend to be more complete as a sentence than a human sentence"

---

## Assistant (Plan · MiMo V2.5 Free · 11.4s)

_Thinking:_

The user wants me to help them frame their thinking into a well-written markdown cell before cell 41. Let me look at what cell 41 is. Let me check the notebook structure again.

Looking at the notebook, cell 41 is around the review length filtering section. Let me find the exact cell.

From my reading:
- Cell 19 (line 1083): `amazon_df = amazon_df[amazon_df["review"].str.len() > 0].reset_index(drop=True)` - removes empty reviews
- Cell 20 (line 1103): `yelp_df = yelp_df[yelp_df["review"].str.len() > 0].reset_index(drop=True)` - removes empty reviews


- Cell 26 (line 1959): `yelp_sample = yelp_sample[yelp_sample["review"].str.len() >= 20]` - filters reviews under 20 chars
- Cell 27 (line 1969): `amazon_df=amazon_df[amazon_df["review"].str.len() >= 20]` - filters reviews under 20 chars

So cell 41 comes after these filtering steps. I need to create a markdown cell that explains the reasoning behind removing short reviews before cell 41.

The key insight is that very short reviews don't contain enough linguistic signal to reliably distinguish between human-written and AI-generated text. Since AI tends to produce more complete, grammatically polished sentences, short reviews could be misleading—either human or AI reviews might look similar when they're too brief. Filtering them out ensures the model learns from reviews with enough content to make meaningful distinctions.

Here's a polished version of your thinking for a markdown cell before the review length filtering:

---

### Review Length Filtering

When detecting AI-generated reviews, very short texts (under ~20 characters) provide insufficient linguistic signal to reliably distinguish between human and AI authorship. Additionally, AI-generated text tends to produce more complete, grammatically polished sentences compared to typical human reviews. Removing excessively short reviews ensures the model trains on text that carries meaningful stylistic cues, reducing noise and improving classification accuracy.

---

Want me to tweak the wording or length?

---

## User

dont mention the under 20 character at start thats what im trying to check what should be the appriate length from which i should keep the review for further analysis and model training

---

## Assistant (Plan · MiMo V2.5 Free · 11.8s)

_Thinking:_

The user wants me to help them frame the markdown cell without mentioning the specific threshold (20 characters). They want to explore what the appropriate minimum review length should be.Let me re-read the notebook to understand what exploration they did around review lengths. From the notebook:

- Cell 24 (line 1244): Amazon stats - Average Review Length: 339.9, Shortest: 4, Longest: 2095
- Cell 25 (line 1328): Shows Amazon reviews with < 20 characters
- Cell 26 (line 1485): Shows Amazon reviews with > 300 characters
- Cell 27 (line 1506): Yelp stats - Average Review Length: 529.9, Shortest: 1, Longest: 4907


- Cell 28 (line 1644): Shows Yelp reviews with < 40 characters
- Cell 29 (line 1786): Shows Yelp reviews with < 20 characters (with review_length column)
- Cell 30 (line 1948): Shows Yelp reviews with > 500 characters

They're filtering reviews at 20 characters minimum, and the user wants the markdown to reflect this is an exploratory step to determine the right threshold rather than a fixed decision. I should frame this as investigating what minimum length makes sense for distinguishing AI from human reviews.

Got it. Here's a revised version without the specific threshold — framed as the reasoning behind the exploration:

---

### Review Length Filtering

When detecting AI-generated reviews, very short texts provide insufficient linguistic signal to reliably distinguish between human and AI authorship. Additionally, AI-generated text tends to produce more complete, grammatically polished sentences compared to typical human reviews. Removing excessively short reviews ensures the model trains on text that carries meaningful stylistic cues, reducing noise and improving classification accuracy.

---

Does this work, or do you want to adjust the tone further?

---

## User

can you now look and read the notebook i have also given markdown and my observation give me what should i do next 

---

## Assistant (Plan · MiMo V2.5 Free · 9.6s)

_Thinking:_

The user wants me to re-read the notebook to see what markdown cells and observations they've already added, and then tell them what they should do next. Let me read the notebook again to see the current state.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "limit": 500
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
1: {
2:  "cells": [
3:   {
4:    "cell_type": "code",
5:    "execution_count": 508,
6:    "id": "ceb271b9",
7:    "metadata": {},
8:    "outputs": [
9:     {
10:      "name": "stdout",
11:      "output_type": "stream",
12:      "text": [
13:       "Amazon shape: (40432, 4)\n",
14:       "Yelp shape: (359052, 6)\n"
15:      ]
16:     }
17:    ],
18:    "source": [
19:     "import pandas as pd\n",
20:     "import numpy as np\n",
21:     "import re\n",
22:     "from sklearn.utils import resample\n",
23:     "from sklearn.model_selection import train_test_split\n",
24:     "from sklearn.metrics import accuracy_score\n",
25:     "import nltk\n",
26:     "from nltk.corpus import stopwords\n",
27:     "from nltk.stem import PorterStemmer\n",
28:     "\n",
29:     "# Load datasets\n",
30:     "amazon_df = pd.read_csv('fake reviews dataset.csv')\n",
31:     "yelp_df = pd.read_csv('Labelled Yelp Dataset.csv')\n",
32:     "\n",
33:     "# Quick view\n",
34:     "print(\"Amazon shape:\", amazon_df.shape)\n",
35:     "print(\"Yelp shape:\", yelp_df.shape)\n"
36:    ]
37:   },
38:   {
39:    "cell_type": "code",
40:    "execution_count": 509,
41:    "id": "aa9d3b06",
42:    "metadata": {},
43:    "outputs": [],
44:    "source": [
45:     "pd.set_option(\"display.max_columns\", None)\n",
46:     "pd.set_option(\"display.max_colwidth\", 200)"
47:    ]
48:   },
49:   {
50:    "cell_type": "code",
51:    "execution_count": 510,
52:    "id": "55238bc3",
53:    "metadata": {},
54:    "outputs": [
55:     {
56:      "data": {
57:       "text/html": [
58:        "<div>\n",
59:        "<style scoped>\n",
60:        "    .dataframe tbody tr th:only-of-type {\n",
61:        "        vertical-align: middle;\n",
62:        "    }\n",
63:        "\n",
64:        "    .dataframe tbody tr th {\n",
65:        "        vertical-align: top;\n",
66:        "    }\n",
67:        "\n",
68:        "    .dataframe thead th {\n",
69:        "        text-align: right;\n",
70:        "    }\n",
71:        "</style>\n",
72:        "<table border=\"1\" class=\"dataframe\">\n",
73:        "  <thead>\n",
74:        "    <tr style=\"text-align: right;\">\n",
75:        "      <th></th>\n",
76:        "      <th>category</th>\n",
77:        "      <th>rating</th>\n",
78:        "      <th>label</th>\n",
79:        "      <th>text_</th>\n",
80:        "    </tr>\n",
81:        "  </thead>\n",
82:        "  <tbody>\n",
83:        "    <tr>\n",
84:        "      <th>0</th>\n",
85:        "      <td>Home_and_Kitchen_5</td>\n",
86:        "      <td>5.0</td>\n",
87:        "      <td>CG</td>\n",
88:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
89:        "    </tr>\n",
90:        "    <tr>\n",
91:        "      <th>1</th>\n",
92:        "      <td>Home_and_Kitchen_5</td>\n",
93:        "      <td>5.0</td>\n",
94:        "      <td>CG</td>\n",
95:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
96:        "    </tr>\n",
97:        "    <tr>\n",
98:        "      <th>2</th>\n",
99:        "      <td>Home_and_Kitchen_5</td>\n",
100:        "      <td>5.0</td>\n",
101:        "      <td>CG</td>\n",
102:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
103:        "    </tr>\n",
104:        "    <tr>\n",
105:        "      <th>3</th>\n",
106:        "      <td>Home_and_Kitchen_5</td>\n",
107:        "      <td>1.0</td>\n",
108:        "      <td>CG</td>\n",
109:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
110:        "    </tr>\n",
111:        "    <tr>\n",
112:        "      <th>4</th>\n",
113:        "      <td>Home_and_Kitchen_5</td>\n",
114:        "      <td>5.0</td>\n",
115:        "      <td>CG</td>\n",
116:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
117:        "    </tr>\n",
118:        "  </tbody>\n",
119:        "</table>\n",
120:        "</div>"
121:       ],
122:       "text/plain": [
123:        "             category  rating label  \\\n",
124:        "0  Home_and_Kitchen_5     5.0    CG   \n",
125:        "1  Home_and_Kitchen_5     5.0    CG   \n",
126:        "2  Home_and_Kitchen_5     5.0    CG   \n",
127:        "3  Home_and_Kitchen_5     1.0    CG   \n",
128:        "4  Home_and_Kitchen_5     5.0    CG   \n",
129:        "\n",
130:        "                                                                                   text_  \n",
131:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty  \n",
132:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years  \n",
133:        "2                    This pillow saved my back. I love the look and feel of this pillow.  \n",
134:        "3      Missing information on how to use it, but it is a great product for the price!  I  \n",
135:        "4  Very nice set. Good quality. We have had the set for two months now and have not been  "
136:       ]
137:      },
138:      "execution_count": 510,
139:      "metadata": {},
140:      "output_type": "execute_result"
141:     }
142:    ],
143:    "source": [
144:     "amazon_df.head()"
145:    ]
146:   },
147:   {
148:    "cell_type": "code",
149:    "execution_count": 511,
150:    "id": "7800c77e",
151:    "metadata": {},
152:    "outputs": [
153:     {
154:      "data": {
155:       "text/html": [
156:        "<div>\n",
157:        "<style scoped>\n",
158:        "    .dataframe tbody tr th:only-of-type {\n",
159:        "        vertical-align: middle;\n",
160:        "    }\n",
161:        "\n",
162:        "    .dataframe tbody tr th {\n",
163:        "        vertical-align: top;\n",
164:        "    }\n",
165:        "\n",
166:        "    .dataframe thead th {\n",
167:        "        text-align: right;\n",
168:        "    }\n",
169:        "</style>\n",
170:        "<table border=\"1\" class=\"dataframe\">\n",
171:        "  <thead>\n",
172:        "    <tr style=\"text-align: right;\">\n",
173:        "      <th></th>\n",
174:        "      <th>User_id</th>\n",
175:        "      <th>Product_id</th>\n",
176:        "      <th>Rating</th>\n",
177:        "      <th>Date</th>\n",
178:        "      <th>Review</th>\n",
179:        "      <th>Label</th>\n",
180:        "    </tr>\n",
181:        "  </thead>\n",
182:        "  <tbody>\n",
183:        "    <tr>\n",
184:        "      <th>0</th>\n",
185:        "      <td>923</td>\n",
186:        "      <td>0</td>\n",
187:        "      <td>3</td>\n",
188:        "      <td>12/8/2014</td>\n",
189:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
190:        "      <td>-1</td>\n",
191:        "    </tr>\n",
192:        "    <tr>\n",
193:        "      <th>1</th>\n",
194:        "      <td>924</td>\n",
195:        "      <td>0</td>\n",
196:        "      <td>3</td>\n",
197:        "      <td>5/16/2013</td>\n",
198:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
199:        "      <td>-1</td>\n",
200:        "    </tr>\n",
201:        "    <tr>\n",
202:        "      <th>2</th>\n",
203:        "      <td>925</td>\n",
204:        "      <td>0</td>\n",
205:        "      <td>4</td>\n",
206:        "      <td>7/1/2013</td>\n",
207:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
208:        "      <td>-1</td>\n",
209:        "    </tr>\n",
210:        "    <tr>\n",
211:        "      <th>3</th>\n",
212:        "      <td>926</td>\n",
213:        "      <td>0</td>\n",
214:        "      <td>4</td>\n",
215:        "      <td>7/28/2011</td>\n",
216:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
217:        "      <td>-1</td>\n",
218:        "    </tr>\n",
219:        "    <tr>\n",
220:        "      <th>4</th>\n",
221:        "      <td>927</td>\n",
222:        "      <td>0</td>\n",
223:        "      <td>4</td>\n",
224:        "      <td>11/1/2010</td>\n",
225:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
226:        "      <td>-1</td>\n",
227:        "    </tr>\n",
228:        "  </tbody>\n",
229:        "</table>\n",
230:        "</div>"
231:       ],
232:       "text/plain": [
233:        "   User_id  Product_id  Rating       Date  \\\n",
234:        "0      923           0       3  12/8/2014   \n",
235:        "1      924           0       3  5/16/2013   \n",
236:        "2      925           0       4   7/1/2013   \n",
237:        "3      926           0       4  7/28/2011   \n",
238:        "4      927           0       4  11/1/2010   \n",
239:        "\n",
240:        "                                                                                                                                                                                                    Review  \\\n",
241:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
242:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
243:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
244:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
245:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
246:        "\n",
247:        "   Label  \n",
248:        "0     -1  \n",
249:        "1     -1  \n",
250:        "2     -1  \n",
251:        "3     -1  \n",
252:        "4     -1  "
253:       ]
254:      },
255:      "execution_count": 511,
256:      "metadata": {},
257:      "output_type": "execute_result"
258:     }
259:    ],
260:    "source": [
261:     "yelp_df.head()"
262:    ]
263:   },
264:   {
265:    "cell_type": "code",
266:    "execution_count": 512,
267:    "id": "9af9b883",
268:    "metadata": {},
269:    "outputs": [
270:     {
271:      "name": "stdout",
272:      "output_type": "stream",
273:      "text": [
274:       "Column Names:\n",
275:       "\n",
276:       "['category', 'rating', 'label', 'text_']\n",
277:       "\n",
278:       "Dataset Info:\n",
279:       "\n",
280:       "<class 'pandas.DataFrame'>\n",
281:       "RangeIndex: 40432 entries, 0 to 40431\n",
282:       "Data columns (total 4 columns):\n",
283:       " #   Column    Non-Null Count  Dtype  \n",
284:       "---  ------    --------------  -----  \n",
285:       " 0   category  40432 non-null  str    \n",
286:       " 1   rating    40432 non-null  float64\n",
287:       " 2   label     40432 non-null  str    \n",
288:       " 3   text_     40432 non-null  str    \n",
289:       "dtypes: float64(1), str(3)\n",
290:       "memory usage: 15.5 MB\n",
291:       "\n",
292:       "Missing Values:\n",
293:       "\n",
294:       "category    0\n",
295:       "rating      0\n",
296:       "label       0\n",
297:       "text_       0\n",
298:       "dtype: int64\n"
299:      ]
300:     }
301:    ],
302:    "source": [
303:     "print(\"Column Names:\\n\")\n",
304:     "print(amazon_df.columns.tolist())\n",
305:     "\n",
306:     "print(\"\\nDataset Info:\\n\")\n",
307:     "amazon_df.info()\n",
308:     "\n",
309:     "print(\"\\nMissing Values:\\n\")\n",
310:     "print(amazon_df.isnull().sum())"
311:    ]
312:   },
313:   {
314:    "cell_type": "code",
315:    "execution_count": 513,
316:    "id": "f9678399",
317:    "metadata": {},
318:    "outputs": [
319:     {
320:      "name": "stdout",
321:      "output_type": "stream",
322:      "text": [
323:       "Column Names:\n",
324:       "\n",
325:       "['User_id', 'Product_id', 'Rating', 'Date', 'Review', 'Label']\n",
326:       "\n",
327:       "Dataset Info:\n",
328:       "\n",
329:       "<class 'pandas.DataFrame'>\n",
330:       "RangeIndex: 359052 entries, 0 to 359051\n",
331:       "Data columns (total 6 columns):\n",
332:       " #   Column      Non-Null Count   Dtype\n",
333:       "---  ------      --------------   -----\n",
334:       " 0   User_id     359052 non-null  int64\n",
335:       " 1   Product_id  359052 non-null  int64\n",
336:       " 2   Rating      359052 non-null  int64\n",
337:       " 3   Date        359052 non-null  str  \n",
338:       " 4   Review      359052 non-null  str  \n",
339:       " 5   Label       359052 non-null  int64\n",
340:       "dtypes: int64(4), str(2)\n",
341:       "memory usage: 239.0 MB\n",
342:       "\n",
343:       "Missing Values:\n",
344:       "\n",
345:       "User_id       0\n",
346:       "Product_id    0\n",
347:       "Rating        0\n",
348:       "Date          0\n",
349:       "Review        0\n",
350:       "Label         0\n",
351:       "dtype: int64\n"
352:      ]
353:     }
354:    ],
355:    "source": [
356:     "print(\"Column Names:\\n\")\n",
357:     "print(yelp_df.columns.tolist())\n",
358:     "\n",
359:     "print(\"\\nDataset Info:\\n\")\n",
360:     "yelp_df.info()\n",
361:     "\n",
362:     "print(\"\\nMissing Values:\\n\")\n",
363:     "print(yelp_df.isnull().sum())"
364:    ]
365:   },
366:   {
367:    "cell_type": "markdown",
368:    "id": "9c6f6dbe",
369:    "metadata": {},
370:    "source": [
371:     "### Label Encoding"
372:    ]
373:   },
374:   {
375:    "cell_type": "markdown",
376:    "id": "9ba41eba",
377:    "metadata": {},
378:    "source": [
379:     " 1 = fake/AI-generated, 0 = genuine"
380:    ]
381:   },
382:   {
383:    "cell_type": "code",
384:    "execution_count": 514,
385:    "id": "d9a08569",
386:    "metadata": {},
387:    "outputs": [
388:     {
389:      "data": {
390:       "text/html": [
391:        "<div>\n",
392:        "<style scoped>\n",
393:        "    .dataframe tbody tr th:only-of-type {\n",
394:        "        vertical-align: middle;\n",
395:        "    }\n",
396:        "\n",
397:        "    .dataframe tbody tr th {\n",
398:        "        vertical-align: top;\n",
399:        "    }\n",
400:        "\n",
401:        "    .dataframe thead th {\n",
402:        "        text-align: right;\n",
403:        "    }\n",
404:        "</style>\n",
405:        "<table border=\"1\" class=\"dataframe\">\n",
406:        "  <thead>\n",
407:        "    <tr style=\"text-align: right;\">\n",
408:        "      <th></th>\n",
409:        "      <th>category</th>\n",
410:        "      <th>rating</th>\n",
411:        "      <th>label</th>\n",
412:        "      <th>text_</th>\n",
413:        "    </tr>\n",
414:        "  </thead>\n",
415:        "  <tbody>\n",
416:        "    <tr>\n",
417:        "      <th>0</th>\n",
418:        "      <td>Home_and_Kitchen_5</td>\n",
419:        "      <td>5.0</td>\n",
420:        "      <td>1</td>\n",
421:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
422:        "    </tr>\n",
423:        "    <tr>\n",
424:        "      <th>1</th>\n",
425:        "      <td>Home_and_Kitchen_5</td>\n",
426:        "      <td>5.0</td>\n",
427:        "      <td>1</td>\n",
428:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
429:        "    </tr>\n",
430:        "    <tr>\n",
431:        "      <th>2</th>\n",
432:        "      <td>Home_and_Kitchen_5</td>\n",
433:        "      <td>5.0</td>\n",
434:        "      <td>1</td>\n",
435:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
436:        "    </tr>\n",
437:        "    <tr>\n",
438:        "      <th>3</th>\n",
439:        "      <td>Home_and_Kitchen_5</td>\n",
440:        "      <td>1.0</td>\n",
441:        "      <td>1</td>\n",
442:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
443:        "    </tr>\n",
444:        "    <tr>\n",
445:        "      <th>4</th>\n",
446:        "      <td>Home_and_Kitchen_5</td>\n",
447:        "      <td>5.0</td>\n",
448:        "      <td>1</td>\n",
449:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
450:        "    </tr>\n",
451:        "  </tbody>\n",
452:        "</table>\n",
453:        "</div>"
454:       ],
455:       "text/plain": [
456:        "             category  rating  label  \\\n",
457:        "0  Home_and_Kitchen_5     5.0      1   \n",
458:        "1  Home_and_Kitchen_5     5.0      1   \n",
459:        "2  Home_and_Kitchen_5     5.0      1   \n",
460:        "3  Home_and_Kitchen_5     1.0      1   \n",
461:        "4  Home_and_Kitchen_5     5.0      1   \n",
462:        "\n",
463:        "                                                                                   text_  \n",
464:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty  \n",
465:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years  \n",
466:        "2                    This pillow saved my back. I love the look and feel of this pillow.  \n",
467:        "3      Missing information on how to use it, but it is a great product for the price!  I  \n",
468:        "4  Very nice set. Good quality. We have had the set for two months now and have not been  "
469:       ]
470:      },
471:      "execution_count": 514,
472:      "metadata": {},
473:      "output_type": "execute_result"
474:     }
475:    ],
476:    "source": [
477:     "label_map={'CG':1,'OR':0}\n",
478:     "amazon_df['label']=amazon_df['label'].map(label_map)\n",
479:     "amazon_df.head()"
480:    ]
481:   },
482:   {
483:    "cell_type": "markdown",
484:    "id": "4a3ccf6b",
485:    "metadata": {},
486:    "source": [
487:     " ### Column Standardization"
488:    ]
489:   },
490:   {
491:    "cell_type": "code",
492:    "execution_count": 515,
493:    "id": "489d777d",
494:    "metadata": {},
495:    "outputs": [
496:     {
497:      "data": {
498:       "text/html": [
499:        "<div>\n",
500:        "<style scoped>\n",

(Showing lines 1-500 of 5229. Use offset=501 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 5.8s)

_Thinking:_

Let me continue reading the notebook to see all the markdown cells the user has added.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 501,
  "limit": 1500
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
501:        "    .dataframe tbody tr th:only-of-type {\n",
502:        "        vertical-align: middle;\n",
503:        "    }\n",
504:        "\n",
505:        "    .dataframe tbody tr th {\n",
506:        "        vertical-align: top;\n",
507:        "    }\n",
508:        "\n",
509:        "    .dataframe thead th {\n",
510:        "        text-align: right;\n",
511:        "    }\n",
512:        "</style>\n",
513:        "<table border=\"1\" class=\"dataframe\">\n",
514:        "  <thead>\n",
515:        "    <tr style=\"text-align: right;\">\n",
516:        "      <th></th>\n",
517:        "      <th>rating</th>\n",
518:        "      <th>review</th>\n",
519:        "      <th>label</th>\n",
520:        "    </tr>\n",
521:        "  </thead>\n",
522:        "  <tbody>\n",
523:        "    <tr>\n",
524:        "      <th>0</th>\n",
525:        "      <td>5.0</td>\n",
526:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
527:        "      <td>1</td>\n",
528:        "    </tr>\n",
529:        "    <tr>\n",
530:        "      <th>1</th>\n",
531:        "      <td>5.0</td>\n",
532:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
533:        "      <td>1</td>\n",
534:        "    </tr>\n",
535:        "    <tr>\n",
536:        "      <th>2</th>\n",
537:        "      <td>5.0</td>\n",
538:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
539:        "      <td>1</td>\n",
540:        "    </tr>\n",
541:        "    <tr>\n",
542:        "      <th>3</th>\n",
543:        "      <td>1.0</td>\n",
544:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
545:        "      <td>1</td>\n",
546:        "    </tr>\n",
547:        "    <tr>\n",
548:        "      <th>4</th>\n",
549:        "      <td>5.0</td>\n",
550:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
551:        "      <td>1</td>\n",
552:        "    </tr>\n",
553:        "  </tbody>\n",
554:        "</table>\n",
555:        "</div>"
556:       ],
557:       "text/plain": [
558:        "   rating  \\\n",
559:        "0     5.0   \n",
560:        "1     5.0   \n",
561:        "2     5.0   \n",
562:        "3     1.0   \n",
563:        "4     5.0   \n",
564:        "\n",
565:        "                                                                                  review  \\\n",
566:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty   \n",
567:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years   \n",
568:        "2                    This pillow saved my back. I love the look and feel of this pillow.   \n",
569:        "3      Missing information on how to use it, but it is a great product for the price!  I   \n",
570:        "4  Very nice set. Good quality. We have had the set for two months now and have not been   \n",
571:        "\n",
572:        "   label  \n",
573:        "0      1  \n",
574:        "1      1  \n",
575:        "2      1  \n",
576:        "3      1  \n",
577:        "4      1  "
578:       ]
579:      },
580:      "execution_count": 515,
581:      "metadata": {},
582:      "output_type": "execute_result"
583:     }
584:    ],
585:    "source": [
586:     "#Amazon rename and remove unwanted columns\n",
587:     "\n",
588:     "amazon_df = amazon_df.rename(columns={\n",
589:     "    \"text_\": \"review\"\n",
590:     "})\n",
591:     " \n",
592:     "amazon_df = amazon_df[[\"rating\",\"review\",\"label\"]]\n",
593:     "\n",
594:     "amazon_df.head()"
595:    ]
596:   },
597:   {
598:    "cell_type": "code",
599:    "execution_count": 516,
600:    "id": "a652d43b",
601:    "metadata": {},
602:    "outputs": [
603:     {
604:      "data": {
605:       "text/html": [
606:        "<div>\n",
607:        "<style scoped>\n",
608:        "    .dataframe tbody tr th:only-of-type {\n",
609:        "        vertical-align: middle;\n",
610:        "    }\n",
611:        "\n",
612:        "    .dataframe tbody tr th {\n",
613:        "        vertical-align: top;\n",
614:        "    }\n",
615:        "\n",
616:        "    .dataframe thead th {\n",
617:        "        text-align: right;\n",
618:        "    }\n",
619:        "</style>\n",
620:        "<table border=\"1\" class=\"dataframe\">\n",
621:        "  <thead>\n",
622:        "    <tr style=\"text-align: right;\">\n",
623:        "      <th></th>\n",
624:        "      <th>rating</th>\n",
625:        "      <th>review</th>\n",
626:        "      <th>label</th>\n",
627:        "    </tr>\n",
628:        "  </thead>\n",
629:        "  <tbody>\n",
630:        "    <tr>\n",
631:        "      <th>0</th>\n",
632:        "      <td>3</td>\n",
633:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
634:        "      <td>-1</td>\n",
635:        "    </tr>\n",
636:        "    <tr>\n",
637:        "      <th>1</th>\n",
638:        "      <td>3</td>\n",
639:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
640:        "      <td>-1</td>\n",
641:        "    </tr>\n",
642:        "    <tr>\n",
643:        "      <th>2</th>\n",
644:        "      <td>4</td>\n",
645:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
646:        "      <td>-1</td>\n",
647:        "    </tr>\n",
648:        "    <tr>\n",
649:        "      <th>3</th>\n",
650:        "      <td>4</td>\n",
651:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
652:        "      <td>-1</td>\n",
653:        "    </tr>\n",
654:        "    <tr>\n",
655:        "      <th>4</th>\n",
656:        "      <td>4</td>\n",
657:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
658:        "      <td>-1</td>\n",
659:        "    </tr>\n",
660:        "  </tbody>\n",
661:        "</table>\n",
662:        "</div>"
663:       ],
664:       "text/plain": [
665:        "   rating  \\\n",
666:        "0       3   \n",
667:        "1       3   \n",
668:        "2       4   \n",
669:        "3       4   \n",
670:        "4       4   \n",
671:        "\n",
672:        "                                                                                                                                                                                                    review  \\\n",
673:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
674:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
675:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
676:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
677:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
678:        "\n",
679:        "   label  \n",
680:        "0     -1  \n",
681:        "1     -1  \n",
682:        "2     -1  \n",
683:        "3     -1  \n",
684:        "4     -1  "
685:       ]
686:      },
687:      "execution_count": 516,
688:      "metadata": {},
689:      "output_type": "execute_result"
690:     }
691:    ],
692:    "source": [
693:     "#Yelp rename and remove unwanted columns\n",
694:     "\n",
695:     "yelp_df=yelp_df.rename(columns={\n",
696:     "    \"Rating\":\"rating\",\n",
697:     "    \"Review\":\"review\",\n",
698:     "    \"Label\":\"label\"\n",
699:     "})\n",
700:     "\n",
701:     "yelp_df=yelp_df[[\"rating\",\"review\",\"label\"]]\n",
702:     "\n",
703:     "yelp_df.head()"
704:    ]
705:   },
706:   {
707:    "cell_type": "code",
708:    "execution_count": 517,
709:    "id": "23166f6e",
710:    "metadata": {},
711:    "outputs": [
712:     {
713:      "data": {
714:       "text/html": [
715:        "<div>\n",
716:        "<style scoped>\n",
717:        "    .dataframe tbody tr th:only-of-type {\n",
718:        "        vertical-align: middle;\n",
719:        "    }\n",
720:        "\n",
721:        "    .dataframe tbody tr th {\n",
722:        "        vertical-align: top;\n",
723:        "    }\n",
724:        "\n",
725:        "    .dataframe thead th {\n",
726:        "        text-align: right;\n",
727:        "    }\n",
728:        "</style>\n",
729:        "<table border=\"1\" class=\"dataframe\">\n",
730:        "  <thead>\n",
731:        "    <tr style=\"text-align: right;\">\n",
732:        "      <th></th>\n",
733:        "      <th>rating</th>\n",
734:        "      <th>review</th>\n",
735:        "      <th>label</th>\n",
736:        "    </tr>\n",
737:        "  </thead>\n",
738:        "  <tbody>\n",
739:        "    <tr>\n",
740:        "      <th>0</th>\n",
741:        "      <td>3</td>\n",
742:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
743:        "      <td>1</td>\n",
744:        "    </tr>\n",
745:        "    <tr>\n",
746:        "      <th>1</th>\n",
747:        "      <td>3</td>\n",
748:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
749:        "      <td>1</td>\n",
750:        "    </tr>\n",
751:        "    <tr>\n",
752:        "      <th>2</th>\n",
753:        "      <td>4</td>\n",
754:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
755:        "      <td>1</td>\n",
756:        "    </tr>\n",
757:        "    <tr>\n",
758:        "      <th>3</th>\n",
759:        "      <td>4</td>\n",
760:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
761:        "      <td>1</td>\n",
762:        "    </tr>\n",
763:        "    <tr>\n",
764:        "      <th>4</th>\n",
765:        "      <td>4</td>\n",
766:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
767:        "      <td>1</td>\n",
768:        "    </tr>\n",
769:        "  </tbody>\n",
770:        "</table>\n",
771:        "</div>"
772:       ],
773:       "text/plain": [
774:        "   rating  \\\n",
775:        "0       3   \n",
776:        "1       3   \n",
777:        "2       4   \n",
778:        "3       4   \n",
779:        "4       4   \n",
780:        "\n",
781:        "                                                                                                                                                                                                    review  \\\n",
782:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
783:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
784:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
785:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
786:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
787:        "\n",
788:        "   label  \n",
789:        "0      1  \n",
790:        "1      1  \n",
791:        "2      1  \n",
792:        "3      1  \n",
793:        "4      1  "
794:       ]
795:      },
796:      "execution_count": 517,
797:      "metadata": {},
798:      "output_type": "execute_result"
799:     }
800:    ],
801:    "source": [
802:     "label_map={-1:1,1:0}\n",
803:     "yelp_df['label']=yelp_df['label'].map(label_map)\n",
804:     "yelp_df.head()"
805:    ]
806:   },
807:   {
808:    "cell_type": "code",
809:    "execution_count": 518,
810:    "id": "1e220dea",
811:    "metadata": {},
812:    "outputs": [
813:     {
814:      "name": "stdout",
815:      "output_type": "stream",
816:      "text": [
817:       "<class 'pandas.DataFrame'>\n",
818:       "RangeIndex: 40432 entries, 0 to 40431\n",
819:       "Data columns (total 3 columns):\n",
820:       " #   Column  Non-Null Count  Dtype  \n",
821:       "---  ------  --------------  -----  \n",
822:       " 0   rating  40432 non-null  float64\n",
823:       " 1   review  40432 non-null  str    \n",
824:       " 2   label   40432 non-null  int64  \n",
825:       "dtypes: float64(1), int64(1), str(1)\n",
826:       "memory usage: 14.5 MB\n"
827:      ]
828:     }
829:    ],
830:    "source": [
831:     "amazon_df.info()"
832:    ]
833:   },
834:   {
835:    "cell_type": "code",
836:    "execution_count": 519,
837:    "id": "f27d1399",
838:    "metadata": {},
839:    "outputs": [
840:     {
841:      "data": {
842:       "text/plain": [
843:        "array([5., 1., 3., 2., 4.])"
844:       ]
845:      },
846:      "execution_count": 519,
847:      "metadata": {},
848:      "output_type": "execute_result"
849:     }
850:    ],
851:    "source": [
852:     "amazon_df[\"rating\"].unique()"
853:    ]
854:   },
855:   {
856:    "cell_type": "code",
857:    "execution_count": 520,
858:    "id": "edf61ac9",
859:    "metadata": {},
860:    "outputs": [],
861:    "source": [
862:     "amazon_df[\"rating\"]=amazon_df[\"rating\"].astype(int)"
863:    ]
864:   },
865:   {
866:    "cell_type": "code",
867:    "execution_count": 521,
868:    "id": "7b4ed1e5",
869:    "metadata": {},
870:    "outputs": [
871:     {
872:      "name": "stdout",
873:      "output_type": "stream",
874:      "text": [
875:       "<class 'pandas.DataFrame'>\n",
876:       "RangeIndex: 359052 entries, 0 to 359051\n",
877:       "Data columns (total 3 columns):\n",
878:       " #   Column  Non-Null Count   Dtype\n",
879:       "---  ------  --------------   -----\n",
880:       " 0   rating  359052 non-null  int64\n",
881:       " 1   review  359052 non-null  str  \n",
882:       " 2   label   359052 non-null  int64\n",
883:       "dtypes: int64(2), str(1)\n",
884:       "memory usage: 227.7 MB\n"
885:      ]
886:     }
887:    ],
888:    "source": [
889:     "yelp_df.info()"
890:    ]
891:   },
892:   {
893:    "cell_type": "markdown",
894:    "id": "a45750ff",
895:    "metadata": {},
896:    "source": [
897:     "### Duplicate Removal"
898:    ]
899:   },
900:   {
901:    "cell_type": "code",
902:    "execution_count": 522,
903:    "id": "eb911bf5",
904:    "metadata": {},
905:    "outputs": [
906:     {
907:      "name": "stdout",
908:      "output_type": "stream",
909:      "text": [
910:       "Duplicates Before: 12\n"
911:      ]
912:     }
913:    ],
914:    "source": [
915:     "print(\"Duplicates Before:\", amazon_df.duplicated().sum())"
916:    ]
917:   },
918:   {
919:    "cell_type": "code",
920:    "execution_count": 523,
921:    "id": "09285ccc",
922:    "metadata": {},
923:    "outputs": [
924:     {
925:      "name": "stdout",
926:      "output_type": "stream",
927:      "text": [
928:       "Dataset Shape After Removing Duplicates: (40412, 3)\n"
929:      ]
930:     }
931:    ],
932:    "source": [
933:     "amazon_df = amazon_df.drop_duplicates(subset=\"review\").reset_index(drop=True)\n",
934:     "\n",
935:     "print(\"Dataset Shape After Removing Duplicates:\", amazon_df.shape)"
936:    ]
937:   },
938:   {
939:    "cell_type": "code",
940:    "execution_count": 524,
941:    "id": "579a79b2",
942:    "metadata": {},
943:    "outputs": [
944:     {
945:      "name": "stdout",
946:      "output_type": "stream",
947:      "text": [
948:       "Duplicates Before: 469\n"
949:      ]
950:     }
951:    ],
952:    "source": [
953:     "print(\"Duplicates Before:\", yelp_df.duplicated().sum())"
954:    ]
955:   },
956:   {
957:    "cell_type": "code",
958:    "execution_count": 525,
959:    "id": "e16e34e8",
960:    "metadata": {},
961:    "outputs": [
962:     {
963:      "name": "stdout",
964:      "output_type": "stream",
965:      "text": [
966:       "Dataset Shape After Removing Duplicates: (358156, 3)\n"
967:      ]
968:     }
969:    ],
970:    "source": [
971:     "yelp_df = yelp_df.drop_duplicates(subset=\"review\").reset_index(drop=True)\n",
972:     "\n",
973:     "print(\"Dataset Shape After Removing Duplicates:\", yelp_df.shape)"
974:    ]
975:   },
976:   {
977:    "cell_type": "markdown",
978:    "id": "d6663b71",
979:    "metadata": {},
980:    "source": [
981:     "### Text Cleaning"
982:    ]
983:   },
984:   {
985:    "cell_type": "code",
986:    "execution_count": 526,
987:    "id": "2fe0a1b8",
988:    "metadata": {},
989:    "outputs": [],
990:    "source": [
991:     "def count_patterns(df, column):\n",
992:     "    # Convert column to string (ignore NaN issues)\n",
993:     "    text = df[column].fillna(\"\").astype(str)\n",
994:     "\n",
995:     "    html_count = text.str.contains(r\"<.*?>\", regex=True).sum()\n",
996:     "    url_count = text.str.contains(r\"http\\S+|www\\.\\S+\", regex=True).sum()\n",
997:     "    email_count = text.str.contains(r\"\\S+@\\S+\", regex=True).sum()\n",
998:     "\n",
999:     "    print(f\"Total rows: {len(df)}\")\n",
1000:     "    print(f\"Rows with HTML tags   : {html_count}\")\n",
1001:     "    print(f\"Rows with URLs        : {url_count}\")\n",
1002:     "    print(f\"Rows with Email IDs   : {email_count}\")\n",
1003:     "\n",
1004:     "    return {\n",
1005:     "        \"html_tags\": html_count,\n",
1006:     "        \"urls\": url_count,\n",
1007:     "        \"emails\": email_count\n",
1008:     "    }"
1009:    ]
1010:   },
1011:   {
1012:    "cell_type": "code",
1013:    "execution_count": 527,
1014:    "id": "b083f438",
1015:    "metadata": {},
1016:    "outputs": [
1017:     {
1018:      "name": "stdout",
1019:      "output_type": "stream",
1020:      "text": [
1021:       "Total rows: 40412\n",
1022:       "Rows with HTML tags   : 203\n",
1023:       "Rows with URLs        : 109\n",
1024:       "Rows with Email IDs   : 11\n",
1025:       "{'html_tags': np.int64(203), 'urls': np.int64(109), 'emails': np.int64(11)}\n",
1026:       "Total rows: 358156\n",
1027:       "Rows with HTML tags   : 0\n",
1028:       "Rows with URLs        : 33\n",
1029:       "Rows with Email IDs   : 215\n",
1030:       "{'html_tags': np.int64(0), 'urls': np.int64(33), 'emails': np.int64(215)}\n"
1031:      ]
1032:     }
1033:    ],
1034:    "source": [
1035:     "print(count_patterns(amazon_df, \"review\"))\n",
1036:     "print(count_patterns(yelp_df, \"review\"))"
1037:    ]
1038:   },
1039:   {
1040:    "cell_type": "code",
1041:    "execution_count": 528,
1042:    "id": "7944a5ba",
1043:    "metadata": {},
1044:    "outputs": [],
1045:    "source": [
1046:     "import html\n",
1047:     "\n",
1048:     "def clean_review(text):\n",
1049:     "    # Convert to string\n",
1050:     "    text = str(text)\n",
1051:     "\n",
1052:     "    # Decode HTML entities\n",
1053:     "    text = html.unescape(text)\n",
1054:     "\n",
1055:     "    # Remove HTML tags\n",
1056:     "    text = re.sub(r\"<.*?>\", \" \", text)\n",
1057:     "\n",
1058:     "    # Remove URLs\n",
1059:     "    text = re.sub(r\"http\\\\S+|www\\\\.\\\\S+\", \" \", text)\n",
1060:     "\n",
1061:     "    # Remove email addresses\n",
1062:     "    text = re.sub(r\"\\\\S+@\\\\S+\", \" \", text)\n",
1063:     "\n",
1064:     "    # Fix common encoding artifacts\n",
1065:     "    text = re.sub(r\"[ÂâÃ]+\", \" \", text)\n",
1066:     "    \n",
1067:     "    # Remove all remaining non-ASCII characters (optional)\n",
1068:     "    text = re.sub(r\"[^\\x00-\\x7F]+\", \" \", text)\n",
1069:     "    \n",
1070:     "    # Remove extra spaces/newlines/tabs\n",
1071:     "    text = re.sub(r\"\\\\s+\", \" \", text).strip()\n",
1072:     "    \n",
1073:     "    # Remove newline, tab, and extra whitespace\n",
1074:     "    text = re.sub(r\"\\s+\", \" \", text).strip()\n",
1075:     "\n",
1076:     "    # Remove special symbols/punctuation and replace with a space\n",
1077:     "    text = re.sub(r\"[^\\w\\s]\", \" \", text)\n",
1078:     "\n",
1079:     "    # Collapse multiple spaces created after removing symbols\n",
1080:     "    text = re.sub(r\"\\s+\", \" \", text).strip()\n",
1081:     "    \n",
1082:     "    # Lowercase only\n",
1083:     "    text = text.lower()\n",
1084:     "\n",
1085:     "    return text"
1086:    ]
1087:   },
1088:   {
1089:    "cell_type": "code",
1090:    "execution_count": 529,
1091:    "id": "3f8701e8",
1092:    "metadata": {},
1093:    "outputs": [],
1094:    "source": [
1095:     "amazon_df[\"review\"] = amazon_df[\"review\"].apply(clean_review)"
1096:    ]
1097:   },
1098:   {
1099:    "cell_type": "code",
1100:    "execution_count": 530,
1101:    "id": "6bd5c901",
1102:    "metadata": {},
1103:    "outputs": [],
1104:    "source": [
1105:     "yelp_df[\"review\"] = yelp_df[\"review\"].apply(clean_review)"
1106:    ]
1107:   },
1108:   {
1109:    "cell_type": "code",
1110:    "execution_count": 531,
1111:    "id": "d0355a58",
1112:    "metadata": {},
1113:    "outputs": [
1114:     {
1115:      "name": "stdout",
1116:      "output_type": "stream",
1117:      "text": [
1118:       "Dataset Shape: (40411, 3)\n"
1119:      ]
1120:     }
1121:    ],
1122:    "source": [
1123:     "amazon_df = amazon_df[amazon_df[\"review\"].str.len() > 0].reset_index(drop=True)\n",
1124:     "\n",
1125:     "print(\"Dataset Shape:\", amazon_df.shape)"
1126:    ]
1127:   },
1128:   {
1129:    "cell_type": "code",
1130:    "execution_count": 532,
1131:    "id": "b3467bac",
1132:    "metadata": {},
1133:    "outputs": [
1134:     {
1135:      "name": "stdout",
1136:      "output_type": "stream",
1137:      "text": [
1138:       "Dataset Shape: (358142, 3)\n"
1139:      ]
1140:     }
1141:    ],
1142:    "source": [
1143:     "yelp_df = yelp_df[yelp_df[\"review\"].str.len() > 0].reset_index(drop=True)\n",
1144:     "\n",
1145:     "print(\"Dataset Shape:\", yelp_df.shape)"
1146:    ]
1147:   },
1148:   {
1149:    "cell_type": "markdown",
1150:    "id": "20bcd797",
1151:    "metadata": {},
1152:    "source": [
1153:     "### Class Distribution"
1154:    ]
1155:   },
1156:   {
1157:    "cell_type": "code",
1158:    "execution_count": 533,
1159:    "id": "1977cd89",
1160:    "metadata": {},
1161:    "outputs": [
1162:     {
1163:      "name": "stdout",
1164:      "output_type": "stream",
1165:      "text": [
1166:       "label\n",
1167:       "0    20215\n",
1168:       "1    20196\n",
1169:       "Name: count, dtype: int64\n",
1170:       "\n",
1171:       "Percentage Distribution:\n",
1172:       "label\n",
1173:       "0    50.02\n",
1174:       "1    49.98\n",
1175:       "Name: count, dtype: float64\n"
1176:      ]
1177:     }
1178:    ],
1179:    "source": [
1180:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
1181:     "\n",
1182:     "print(label_counts)\n",
1183:     "\n",
1184:     "print(\"\\nPercentage Distribution:\")\n",
1185:     "print((label_counts / len(amazon_df) * 100).round(2))"
1186:    ]
1187:   },
1188:   {
1189:    "cell_type": "code",
1190:    "execution_count": 534,
1191:    "id": "99f464ee",
1192:    "metadata": {},
1193:    "outputs": [
1194:     {
1195:      "data": {
1196:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAlsAAAH3CAYAAACM85p5AAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAXDZJREFUeJzt3Xd8k9XiBvAnSfce0EGhQBlllV32hqLsUaaCIEPR68Wr13VFvV7HVa8I4k9FRRAQERGloLJlCbRAoczSskdLBx10t2mT9/dHbCR0kLRNT97k+X4+/UDTjCdp2jw957wnCkmSJBARERGRWShFByAiIiKyZixbRERERGbEskVERERkRixbRERERGbEskVERERkRixbRERERGbEskVERERkRixbRERERGbEsmVGFy9exKZNm1BaWirs9s6fP49NmzahPveure/7XRu3bt3Cjh07sGnTJty5c0d0HKojGo0GmzZtQkJCgugoZpGcnIxNmzYhJydHdBSjlZSUYNOmTcjIyBAdhWTqwoUL2LVrl+gYNWInOoBcXL9+HbGxsfrPHR0d4eXlhdatW8Pf37/Sy2zduhUvvvgisrOz4eXlZfRtJSQk4Ny5c5gwYQJUKpXRl6vs9r7//nu8++67KC0thZ1d3X27q8tY0/td35YsWYJFixZh4MCBcHNzQ9u2bdGwYcMK5yv/3vfv37/S73VsbCyuX79u8veLKrr/5+xe/v7+6N+/v1HXU1RUhMmTJ+Ptt9/Ga6+9VpcR9c6fP48LFy7oP7e3t0dAQAA6d+4MR0dHs9xmuejoaEyePBlxcXHo3LmzWW+rrixZsgRffvklLl68WOnX8/PzsWPHDri4uGDkyJH1nM6ypaen4+DBg/rP7e3t4enpiRYtWqBJkya1uu6bN2/i2LFjGD58ODw8PGobtdaqyyNJEkaOHIk//vgDvXv3FpSwZli2jLRnzx7Mnz8f/fr1g7+/P8rKypCRkYFTp04hODgYCxcuxJNPPgmFQqG/TGhoKCIjI+Hg4GDSbW3atAmvv/468vLy4ObmZvTlanp7NVFdxvrMUVMFBQVYtGgRXnnlFfz73/+u9rzl3/vt27fj4YcfrvD1Tz/9FGvWrDH5+0UV3f9zdq+OHTsaXbbqQ/kfMsOHD4e7uzsKCwtx4sQJaDQafP7555gyZYrZbrtx48aIjIy06D9m7pWRkYH33nsPixcvrvL3wrp16/DUU08B0P0xFxoaWp8RLdqZM2cwefJkdOnSBSEhIdBqtcjKysLp06fh4eGBBQsW4J///GeNfucePHgQM2fOxNmzZ9GhQwczpK+7PO3atcOkSZPwz3/+E0eOHBGUsGZYtky0aNEigxfcoqIifPLJJ3jmmWewb98+fP/991AqdbOzY8aMwZgxY+otW33fnqXnqM61a9dQXFzMX+gW6v6fM0u2bNkytGnTBoBudGbYsGGYMWMGwsPD0bx5c7PcZq9evbBp0yazXLc5rFy5EhqNBtOnT6/yPF9//TX69euHs2fP4uuvv8aHH35Yjwnl4YknnsCCBQv0n5eVlWHNmjVYuHAhtm3bht27d8PJyUlgQvObM2cOHnroIRw7dgw9evQQHcdoLFu15OzsjJdffhnFxcV48803MWbMGMyYMQOAbu3SmTNnMG7cONjb2+svU1xcjNOnTyMjIwPNmjVDmzZt9NNPJ06cwPnz5wEAUVFR+h+coUOHwtvbWz91ERkZidLSUsTExCAnJwdjxoyp8vbKFRUV4ciRI9BqtejVqxfc3d0Nvh4bG4vU1FSMHj3a4PT7h3UflLG6HFlZWThx4gTUajXatm2LkJAQg6/ff/8OHz4MtVqNXr16wdPT0+jvS3W3ExMTg3379unvs52dHTw8PDB8+HCjr/9BjH0sAcP7XFJSgiNHjkClUqFv3776qd/i4mJER0ejrKwM/fr1g7Ozc6XXCwAKhQKurq7o0KEDGjdubHC+2jy+8fHx... (line truncated to 2000 chars)
1197:       "text/plain": [
1198:        "<Figure size 600x600 with 1 Axes>"
1199:       ]
1200:      },
1201:      "metadata": {},
1202:      "output_type": "display_data"
1203:     }
1204:    ],
1205:    "source": [
1206:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
1207:     "\n",
1208:     "# Pie chart\n",
1209:     "plt.figure(figsize=(6, 6))\n",
1210:     "\n",
1211:     "plt.pie(\n",
1212:     "    label_counts,\n",
1213:     "    labels=[\"Human (0)\", \"CG (1)\"],\n",
1214:     "    autopct=\"%1.1f%%\",\n",
1215:     "    startangle=90\n",
1216:     ")\n",
1217:     "\n",
1218:     "plt.title(\"Distribution of Human vs Fake Reviews (Amazon Dataset)\")\n",
1219:     "plt.axis(\"equal\")\n",
1220:     "\n",
1221:     "plt.show()"
1222:    ]
1223:   },
1224:   {
1225:    "cell_type": "code",
1226:    "execution_count": 535,
1227:    "id": "c83f6a6e",
1228:    "metadata": {},
1229:    "outputs": [
1230:     {
1231:      "name": "stdout",
1232:      "output_type": "stream",
1233:      "text": [
1234:       "label\n",
1235:       "0    321568\n",
1236:       "1     36574\n",
1237:       "Name: count, dtype: int64\n",
1238:       "\n",
1239:       "Percentage Distribution:\n",
1240:       "label\n",
1241:       "0    89.79\n",
1242:       "1    10.21\n",
1243:       "Name: count, dtype: float64\n"
1244:      ]
1245:     }
1246:    ],
1247:    "source": [
1248:     "label_counts = yelp_df[\"label\"].value_counts().sort_index()\n",
1249:     "\n",
1250:     "print(label_counts)\n",
1251:     "\n",
1252:     "print(\"\\nPercentage Distribution:\")\n",
1253:     "print((label_counts / len(yelp_df) * 100).round(2))"
1254:    ]
1255:   },
1256:   {
1257:    "cell_type": "code",
1258:    "execution_count": 536,
1259:    "id": "9ba9dd68",
1260:    "metadata": {},
1261:    "outputs": [
1262:     {
1263:      "data": {
1264:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAf0AAAH3CAYAAACxV4buAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAYgVJREFUeJzt3Xd4VGXCBfAzk947IaQASSB0CR0p0gJSVCDCUkQFEdQVRdRdy+7qt/ay2BVEwAaidKT3EggtBEINpDdCei+TzLzfHzEDIYX0d8r5PU8eyOTOvWcmkzlz39sUQggBIiIiMnhK2QGIiIiodbD0iYiIjARLn4iIyEiw9ImIiIwES5+IiMhIsPSJiIiMBEufiIjISLD0iYiIjESLl35cXBw2bNiAoqKill5Urcu7fv06NmzYAJVK1SoZasuhq27evIm9e/diw4YNSElJkR2HmtGmTZtw8eJF2TFaRFpaGjZs2ID09HTZUepNrVZj48aNuHnzpuwopKeioqKwY8eORt/ftCETJycnIzQ0VPu9ubk5HBwc0KlTJ7Rr167G++zfvx9PP/00YmNj0aFDh3ovKzo6GuHh4Zg4cSKsrKzqfb+alrdt2za8+uqrSE9Ph6ura73n1ZSMjX3cre2HH37AokWLMHToUDg4OKB9+/Y1/i4rf/eDBg2Cl5dXtZ9fuHABN27caPDvi6q7++/sTs7Ozhg1alS95zV9+nQsXrwYn376aXPFq+L69euIiIjQfm9qaoo2bdogMDCwxV8HERERmDZtGg4dOoQRI0a06LKay/fff4+33noLMTExNf5cpVJh27ZtMDU1xeTJk1s3nI7Lzs7GgQMHtN+bmZnB3t4eHTt2bPJ7bGpqKkJCQjBy5Ei4uLg0MWnT1ZXH3NwcU6dOxdatW/Hggw82fOaiAdavXy8AiIEDB4rg4GAxefJkMWzYMGFvby/8/f3F0qVLRXl5eZX77N+/XwQHB4u0tLSGLEp89dVXAoBITExs0P1qWt4nn3wiAIj09PQGzaspGRv7uFuTWq0WDg4OYvHixfectvJ3/9tvv9X48xdffLFRvy+q7u6/szu//vGPfzRoXiYmJuLll19uoaS3/7ZGjhwpgoODxcSJE0W7du2Eg4ODWLlyZYstVwghIiIiRHBwsLh06VKLLqe55OfnCzc3N/HRRx/VOs1vv/0mAAgA4uTJk62YTvedOXNGABA9evQQwcHBYsqUKWLkyJHCxcVFtGvXTvznP/8RRUVFjZr3n3/+KQCIY8eONXPqxrlXnoULF4ru3bsLjUbT4Hk3aE2/0uLFizFjxgzt9yqVCsuXL8crr7yCvXv34s8//4SpacWsR48ejdGjRzdmMY3S2svT9Rx1SUlJQW5uLgICAmRHoRrc/Xemy95//30MGjQIAFBSUoJJkyZh/vz56NevH3r16tUiy+zZsyc2bNjQIvNuCWvWrEF2djaeeOKJWqf54Ycf0KdPH9y8eRM//PADBg4c2IoJ9cPs2bPx2muvab/XaDRYt24dnnvuOfz55584cuQI7OzsJCZsefPmzcPy5cuxb98+jB07tkH3bVTp383c3ByLFi2CRqPB4sWLsWzZMjz//PMAKrZtnz17FhMmTIC1tbX2PmVlZTh//jzS0tLg7e2Nrl27wszMDABw8eJFnD9/HgCwc+dOODs7AwCGDx+ONm3aaIcUH374YSiVSpw8eRLp6emYMmVKrcurpFKpcOLECZSUlGDQoEFwdHSs8vMLFy4gJiYGU6ZMqXL73cMt98pYV47c3FycPXsWxcXF6Ny5Mzp37lzl53c/vhMnTqCwsBADBgxo0NBTXcsJCwvD8ePHtY95w4YNsLS0xKRJk+o9/3up73MJVH3MAHDixAkIIXD//ffDwsICQMXvLjQ0FCUlJRgyZAhsbW1rnC8AKBQKWFtbo2vXrtWG/pry/EZFReH8+fMICgqCg4NDlZ8VFRVh586d6NGjB7p06QKg... (line truncated to 2000 chars)
1265:       "text/plain": [
1266:        "<Figure size 600x600 with 1 Axes>"
1267:       ]
1268:      },
1269:      "metadata": {},
1270:      "output_type": "display_data"
1271:     }
1272:    ],
1273:    "source": [
1274:     "label_counts = yelp_df[\"label\"].value_counts().sort_index()\n",
1275:     "\n",
1276:     "# Pie chart\n",
1277:     "plt.figure(figsize=(6, 6))\n",
1278:     "\n",
1279:     "plt.pie(\n",
1280:     "    label_counts,\n",
1281:     "    labels=[\"Human (0)\", \"CG (1)\"],\n",
1282:     "    autopct=\"%1.1f%%\",\n",
1283:     "    startangle=90\n",
1284:     ")\n",
1285:     "\n",
1286:     "plt.title(\"Distribution of Human vs Fake Reviews (Amazon Dataset)\")\n",
1287:     "plt.axis(\"equal\")\n",
1288:     "\n",
1289:     "plt.show()"
1290:    ]
1291:   },
1292:   {
1293:    "cell_type": "markdown",
1294:    "id": "55ffc64d",
1295:    "metadata": {},
1296:    "source": [
1297:     "#### Balance Yelp Dataset\n"
1298:    ]
1299:   },
1300:   {
1301:    "cell_type": "markdown",
1302:    "id": "87109c19",
1303:    "metadata": {},
1304:    "source": [
1305:     "randomly sample 25k from each class to create a balanced subset, since the original Yelp data is heavily skewed (~90% genuine)"
1306:    ]
1307:   },
1308:   {
1309:    "cell_type": "code",
1310:    "execution_count": 537,
1311:    "id": "3bdf9942",
1312:    "metadata": {},
1313:    "outputs": [
1314:     {
1315:      "name": "stdout",
1316:      "output_type": "stream",
1317:      "text": [
1318:       "Label counts:\n",
1319:       " label\n",
1320:       "1    25000\n",
1321:       "0    25000\n",
1322:       "Name: count, dtype: int64\n"
1323:      ]
1324:     }
1325:    ],
1326:    "source": [
1327:     "fake = yelp_df[yelp_df['label'] == 0].sample(n=25000, random_state=42)\n",
1328:     "real = yelp_df[yelp_df['label'] == 1].sample(n=25000, random_state=42)\n",
1329:     "\n",
1330:     "yelp_sample = (\n",
1331:     "    pd.concat([fake, real])\n",
1332:     "      .sample(frac=1, random_state=42)   # shuffle\n",
1333:     "      .reset_index(drop=True)\n",
1334:     ")\n",
1335:     "print(\"Label counts:\\n\", yelp_sample['label'].value_counts())"
1336:    ]
1337:   },
1338:   {
1339:    "cell_type": "code",
1340:    "execution_count": 538,
1341:    "id": "f29b9a60",
1342:    "metadata": {},
1343:    "outputs": [
1344:     {
1345:      "name": "stdout",
1346:      "output_type": "stream",
1347:      "text": [
1348:       "Label counts:\n",
1349:       " label\n",
1350:       "0    20215\n",
1351:       "1    20196\n",
1352:       "Name: count, dtype: int64\n"
1353:      ]
1354:     }
1355:    ],
1356:    "source": [
1357:     "print(\"Label counts:\\n\", amazon_df['label'].value_counts())"
1358:    ]
1359:   },
1360:   {
1361:    "cell_type": "markdown",
1362:    "id": "69cc9285",
1363:    "metadata": {},
1364:    "source": [
1365:     "### Review Length Filtering"
1366:    ]
1367:   },
1368:   {
1369:    "cell_type": "code",
1370:    "execution_count": 539,
1371:    "id": "1c3c0c8d",
1372:    "metadata": {},
1373:    "outputs": [
1374:     {
1375:      "name": "stdout",
1376:      "output_type": "stream",
1377:      "text": [
1378:       "Empty Reviews : 0\n",
1379:       "Average Review Length : 339.90292247160426\n",
1380:       "Shortest Review Length : 4\n",
1381:       "Longest Review Length : 2095\n"
1382:      ]
1383:     }
1384:    ],
1385:    "source": [
1386:     "#amazon\n",
1387:     "\n",
1388:     "print(\"Empty Reviews :\", (amazon_df[\"review\"] == \"\").sum())\n",
1389:     "\n",
1390:     "print(\"Average Review Length :\", amazon_df[\"review\"].str.len().mean())\n",
1391:     "\n",
1392:     "print(\"Shortest Review Length :\", amazon_df[\"review\"].str.len().min())\n",
1393:     "\n",
1394:     "print(\"Longest Review Length :\", amazon_df[\"review\"].str.len().max())"
1395:    ]
1396:   },
1397:   {
1398:    "cell_type": "code",
1399:    "execution_count": 540,
1400:    "id": "f5bf54a4",
1401:    "metadata": {},
1402:    "outputs": [
1403:     {
1404:      "data": {
1405:       "text/html": [
1406:        "<div>\n",
1407:        "<style scoped>\n",
1408:        "    .dataframe tbody tr th:only-of-type {\n",
1409:        "        vertical-align: middle;\n",
1410:        "    }\n",
1411:        "\n",
1412:        "    .dataframe tbody tr th {\n",
1413:        "        vertical-align: top;\n",
1414:        "    }\n",
1415:        "\n",
1416:        "    .dataframe thead th {\n",
1417:        "        text-align: right;\n",
1418:        "    }\n",
1419:        "</style>\n",
1420:        "<table border=\"1\" class=\"dataframe\">\n",
1421:        "  <thead>\n",
1422:        "    <tr style=\"text-align: right;\">\n",
1423:        "      <th></th>\n",
1424:        "      <th>rating</th>\n",
1425:        "      <th>review</th>\n",
1426:        "      <th>label</th>\n",
1427:        "    </tr>\n",
1428:        "  </thead>\n",
1429:        "  <tbody>\n",
1430:        "    <tr>\n",
1431:        "      <th>9907</th>\n",
1432:        "      <td>5</td>\n",
1433:        "      <td>input</td>\n",
1434:        "      <td>1</td>\n",
1435:        "    </tr>\n",
1436:        "    <tr>\n",
1437:        "      <th>18615</th>\n",
1438:        "      <td>3</td>\n",
1439:        "      <td>pfister lf 042 prcc</td>\n",
1440:        "      <td>1</td>\n",
1441:        "    </tr>\n",
1442:        "    <tr>\n",
1443:        "      <th>21677</th>\n",
1444:        "      <td>5</td>\n",
1445:        "      <td>well</td>\n",
1446:        "      <td>1</td>\n",
1447:        "    </tr>\n",
1448:        "    <tr>\n",
1449:        "      <th>36815</th>\n",
1450:        "      <td>5</td>\n",
1451:        "      <td>nice elegant watch</td>\n",
1452:        "      <td>1</td>\n",
1453:        "    </tr>\n",
1454:        "  </tbody>\n",
1455:        "</table>\n",
1456:        "</div>"
1457:       ],
1458:       "text/plain": [
1459:        "       rating               review  label\n",
1460:        "9907        5                input      1\n",
1461:        "18615       3  pfister lf 042 prcc      1\n",
1462:        "21677       5                 well      1\n",
1463:        "36815       5   nice elegant watch      1"
1464:       ]
1465:      },
1466:      "execution_count": 540,
1467:      "metadata": {},
1468:      "output_type": "execute_result"
1469:     }
1470:    ],
1471:    "source": [
1472:     "# Print rows where text has fewer than 20 characters\n",
1473:     "amazon_df[amazon_df[\"review\"].str.len() < 20]"
1474:    ]
1475:   },
1476:   {
1477:    "cell_type": "code",
1478:    "execution_count": 541,
1479:    "id": "6f0277ef",
1480:    "metadata": {},
1481:    "outputs": [
1482:     {
1483:      "data": {
1484:       "text/html": [
1485:        "<div>\n",
1486:        "<style scoped>\n",
1487:        "    .dataframe tbody tr th:only-of-type {\n",
1488:        "        vertical-align: middle;\n",
1489:        "    }\n",
1490:        "\n",
1491:        "    .dataframe tbody tr th {\n",
1492:        "        vertical-align: top;\n",
1493:        "    }\n",
1494:        "\n",
1495:        "    .dataframe thead th {\n",
1496:        "        text-align: right;\n",
1497:        "    }\n",
1498:        "</style>\n",
1499:        "<table border=\"1\" class=\"dataframe\">\n",
1500:        "  <thead>\n",
1501:        "    <tr style=\"text-align: right;\">\n",
1502:        "      <th></th>\n",
1503:        "      <th>rating</th>\n",
1504:        "      <th>review</th>\n",
1505:        "      <th>label</th>\n",
1506:        "    </tr>\n",
1507:        "  </thead>\n",
1508:        "  <tbody>\n",
1509:        "    <tr>\n",
1510:        "      <th>2410</th>\n",
1511:        "      <td>1</td>\n",
1512:        "      <td>i had a hard time contacting the manufacturer distributor in order to make sure the measurements were correct the description and the pdf have completely different dimensions in reality these didn...</td>\n",
1513:        "      <td>0</td>\n",
1514:        "    </tr>\n",
1515:        "    <tr>\n",
1516:        "      <th>2578</th>\n",
1517:        "      <td>5</td>\n",
1518:        "      <td>i purchased this bed and have slept on it for the past week i believe in trying things out to make sure my guests won t suffer from backaches etc the aerobed provides a comfortable night s rest i ...</td>\n",
1519:        "      <td>0</td>\n",
1520:        "    </tr>\n",
1521:        "    <tr>\n",
1522:        "      <th>2605</th>\n",
1523:        "      <td>4</td>\n",
1524:        "      <td>after my first night sleeping on a neckbone pillow i ordered another one so my husband could have his own too i could already feel improvement in my neck and shoulder problems after just one night...</td>\n",
1525:        "      <td>0</td>\n",
1526:        "    </tr>\n",
1527:        "    <tr>\n",
1528:        "      <th>2608</th>\n",
1529:        "      <td>5</td>\n",
1530:        "      <td>these canisters are the perfect size for us we use the smallest one for powdered creamer the middle size for instant coffee and the largest size for sugar which we use to refill our smaller sugar ...</td>\n",
1531:        "      <td>0</td>\n",
1532:        "    </tr>\n",
1533:        "    <tr>\n",
1534:        "      <th>2637</th>\n",
1535:        "      <td>5</td>\n",
1536:        "      <td>these are really wonderful they are perfect for strawberry hulling neatly and easily i ve owned a dozen not because they wear out they don t they just seem to wander away when i m not looking fort...</td>\n",
1537:        "      <td>0</td>\n",
1538:        "    </tr>\n",
1539:        "    <tr>\n",
1540:        "      <th>...</th>\n",
1541:        "      <td>...</td>\n",
1542:        "      <td>...</td>\n",
1543:        "      <td>...</td>\n",
1544:        "    </tr>\n",
1545:        "    <tr>\n",
1546:        "      <th>40406</th>\n",
1547:        "      <td>4</td>\n",
1548:        "      <td>i had read some reviews saying that this bra ran small and so i ordered two band and cup sizes up and it was still too small definitely along the lines of a sports bra squish effect the sides do c...</td>\n",
1549:        "      <td>0</td>\n",
1550:        "    </tr>\n",
1551:        "    <tr>\n",
1552:        "      <th>40407</th>\n",
1553:        "      <td>5</td>\n",
1554:        "      <td>i wasn t sure exactly what it would be it is a little large for my small size but i think it is a nice fit the fabric is a nice thin material but it is a little thin in the legs i wish it was thic...</td>\n",
1555:        "      <td>1</td>\n",
1556:        "    </tr>\n",
1557:        "    <tr>\n",
1558:        "      <th>40408</th>\n",
1559:        "      <td>2</td>\n",
1560:        "      <td>you can wear the hood by itself wear it with the hood or wear just the jacket without the hood how is that for 3 in 1 systems reminiscent of what lands end sells as a squall jacket or what uniform...</td>\n",
1561:        "      <td>0</td>\n",
1562:        "    </tr>\n",
1563:        "    <tr>\n",
1564:        "      <th>40409</th>\n",
1565:        "      <td>1</td>\n",
1566:        "      <td>i liked nothing about this dress the only reason i gave it 4 stars is because i ordered the size 6 5 and it fit perfectly the fabric is a nice thin material and the color is vibrant it s a little ...</td>\n",
1567:        "      <td>1</td>\n",
1568:        "    </tr>\n",
1569:        "    <tr>\n",
1570:        "      <th>40410</th>\n",
1571:        "      <td>5</td>\n",
1572:        "      <td>i work in the wedding industry and have to work long days on my feet outside in the heat and have to look professional i ve spent a ridiculous amount of money on high end dress shoes like merrels ...</td>\n",
1573:        "      <td>0</td>\n",
1574:        "    </tr>\n",
1575:        "  </tbody>\n",
1576:        "</table>\n",
1577:        "<p>14050 rows × 3 columns</p>\n",
1578:        "</div>"
1579:       ],
1580:       "text/plain": [
1581:        "       rating  \\\n",
1582:        "2410        1   \n",
1583:        "2578        5   \n",
1584:        "2605        4   \n",
1585:        "2608        5   \n",
1586:        "2637        5   \n",
1587:        "...       ...   \n",
1588:        "40406       4   \n",
1589:        "40407       5   \n",
1590:        "40408       2   \n",
1591:        "40409       1   \n",
1592:        "40410       5   \n",
1593:        "\n",
1594:        "                                                                                                                                                                                                        review  \\\n",
1595:        "2410   i had a hard time contacting the manufacturer distributor in order to make sure the measurements were correct the description and the pdf have completely different dimensions in reality these didn...   \n",
1596:        "2578   i purchased this bed and have slept on it for the past week i believe in trying things out to make sure my guests won t suffer from backaches etc the aerobed provides a comfortable night s rest i ...   \n",
1597:        "2605   after my first night sleeping on a neckbone pillow i ordered another one so my husband could have his own too i could already feel improvement in my neck and shoulder problems after just one night...   \n",
1598:        "2608   these canisters are the perfect size for us we use the smallest one for powdered creamer the middle size for instant coffee and the largest size for sugar which we use to refill our smaller sugar ...   \n",
1599:        "2637   these are really wonderful they are perfect for strawberry hulling neatly and easily i ve owned a dozen not because they wear out they don t they just seem to wander away when i m not looking fort...   \n",
1600:        "...                                                                                                                                                                                                        ...   \n",
1601:        "40406  i had read some reviews saying that this bra ran small and so i ordered two band and cup sizes up and it was still too small definitely along the lines of a sports bra squish effect the sides do c...   \n",
1602:        "40407  i wasn t sure exactly what it would be it is a little large for my small size but i think it is a nice fit the fabric is a nice thin material but it is a little thin in the legs i wish it was thic...   \n",
1603:        "40408  you can wear the hood by itself wear it with the hood or wear just the jacket without the hood how is that for 3 in 1 systems reminiscent of what lands end sells as a squall jacket or what uniform...   \n",
1604:        "40409  i liked nothing about this dress the only reason i gave it 4 stars is because i ordered the size 6 5 and it fit perfectly the fabric is a nice thin material and the color is vibrant it s a little ...   \n",
1605:        "40410  i work in the wedding industry and have to work long days on my feet outside in the heat and have to look professional i ve spent a ridiculous amount of money on high end dress shoes like merrels ...   \n",
1606:        "\n",
1607:        "       label  \n",
1608:        "2410       0  \n",
1609:        "2578       0  \n",
1610:        "2605       0  \n",
1611:        "2608       0  \n",
1612:        "2637       0  \n",
1613:        "...      ...  \n",
1614:        "40406      0  \n",
1615:        "40407      1  \n",
1616:        "40408      0  \n",
1617:        "40409      1  \n",
1618:        "40410      0  \n",
1619:        "\n",
1620:        "[14050 rows x 3 columns]"
1621:       ]
1622:      },
1623:      "execution_count": 541,
1624:      "metadata": {},
1625:      "output_type": "execute_result"
1626:     }
1627:    ],
1628:    "source": [
1629:     "amazon_df[amazon_df[\"review\"].str.len() > 300]"
1630:    ]
1631:   },
1632:   {
1633:    "cell_type": "code",
1634:    "execution_count": 542,
1635:    "id": "37ef9503",
1636:    "metadata": {},
1637:    "outputs": [
1638:     {
1639:      "name": "stdout",
1640:      "output_type": "stream",
1641:      "text": [
1642:       "Label Distribution (Count):\n",
1643:       "label\n",
1644:       "0    7819\n",
1645:       "1    6231\n",
1646:       "Name: count, dtype: int64\n",
1647:       "\n",
1648:       "Label Distribution (Percentage):\n",
1649:       "label\n",
1650:       "0    55.65\n",
1651:       "1    44.35\n",
1652:       "Name: count, dtype: float64\n"
1653:      ]
1654:     }
1655:    ],
1656:    "source": [
1657:     "long_reviews = amazon_df[amazon_df[\"review\"].str.len() >300]\n",
1658:     "\n",
1659:     "# Label counts\n",
1660:     "label_counts = long_reviews[\"label\"].value_counts().sort_index()\n",
1661:     "\n",
1662:     "print(\"Label Distribution (Count):\")\n",
1663:     "print(label_counts)\n",
1664:     "\n",
1665:     "print(\"\\nLabel Distribution (Percentage):\")\n",
1666:     "print((label_counts / len(long_reviews) * 100).round(2))"
1667:    ]
1668:   },
1669:   {
1670:    "cell_type": "code",
1671:    "execution_count": 543,
1672:    "id": "395aa86d",
1673:    "metadata": {},
1674:    "outputs": [
1675:     {
1676:      "name": "stdout",
1677:      "output_type": "stream",
1678:      "text": [
1679:       "Empty Reviews : 0\n",
1680:       "Average Review Length : 529.96384\n",
1681:       "Shortest Review Length : 1\n",
1682:       "Longest Review Length : 4907\n"
1683:      ]
1684:     }
1685:    ],
1686:    "source": [
1687:     "#yelp\n",
1688:     "\n",
1689:     "print(\"Empty Reviews :\", (yelp_sample[\"review\"] == \"\").sum())\n",
1690:     "\n",
1691:     "print(\"Average Review Length :\", yelp_sample[\"review\"].str.len().mean())\n",
1692:     "\n",
1693:     "print(\"Shortest Review Length :\", yelp_sample[\"review\"].str.len().min())\n",
1694:     "\n",
1695:     "print(\"Longest Review Length :\", yelp_sample[\"review\"].str.len().max())"
1696:    ]
1697:   },
1698:   {
1699:    "cell_type": "code",
1700:    "execution_count": 544,
1701:    "id": "02f9e6a4",
1702:    "metadata": {},
1703:    "outputs": [
1704:     {
1705:      "data": {
1706:       "text/html": [
1707:        "<div>\n",
1708:        "<style scoped>\n",
1709:        "    .dataframe tbody tr th:only-of-type {\n",
1710:        "        vertical-align: middle;\n",
1711:        "    }\n",
1712:        "\n",
1713:        "    .dataframe tbody tr th {\n",
1714:        "        vertical-align: top;\n",
1715:        "    }\n",
1716:        "\n",
1717:        "    .dataframe thead th {\n",
1718:        "        text-align: right;\n",
1719:        "    }\n",
1720:        "</style>\n",
1721:        "<table border=\"1\" class=\"dataframe\">\n",
1722:        "  <thead>\n",
1723:        "    <tr style=\"text-align: right;\">\n",
1724:        "      <th></th>\n",
1725:        "      <th>rating</th>\n",
1726:        "      <th>review</th>\n",
1727:        "      <th>label</th>\n",
1728:        "    </tr>\n",
1729:        "  </thead>\n",
1730:        "  <tbody>\n",
1731:        "    <tr>\n",
1732:        "      <th>56</th>\n",
1733:        "      <td>5</td>\n",
1734:        "      <td>still the best</td>\n",
1735:        "      <td>1</td>\n",
1736:        "    </tr>\n",
1737:        "    <tr>\n",
1738:        "      <th>75</th>\n",
1739:        "      <td>5</td>\n",
1740:        "      <td>love this place</td>\n",
1741:        "      <td>1</td>\n",
1742:        "    </tr>\n",
1743:        "    <tr>\n",
1744:        "      <th>421</th>\n",
1745:        "      <td>5</td>\n",
1746:        "      <td>5</td>\n",
1747:        "      <td>1</td>\n",
1748:        "    </tr>\n",
1749:        "    <tr>\n",
1750:        "      <th>854</th>\n",
1751:        "      <td>5</td>\n",
1752:        "      <td>great place</td>\n",
1753:        "      <td>1</td>\n",
1754:        "    </tr>\n",
1755:        "    <tr>\n",
1756:        "      <th>908</th>\n",
1757:        "      <td>3</td>\n",
1758:        "      <td>i like the drinks</td>\n",
1759:        "      <td>1</td>\n",
1760:        "    </tr>\n",
1761:        "    <tr>\n",
1762:        "      <th>...</th>\n",
1763:        "      <td>...</td>\n",
1764:        "      <td>...</td>\n",
1765:        "      <td>...</td>\n",
1766:        "    </tr>\n",
1767:        "    <tr>\n",
1768:        "      <th>49848</th>\n",
1769:        "      <td>5</td>\n",
1770:        "      <td>excellent</td>\n",
1771:        "      <td>1</td>\n",
1772:        "    </tr>\n",
1773:        "    <tr>\n",
1774:        "      <th>49858</th>\n",
1775:        "      <td>5</td>\n",
1776:        "      <td>love it</td>\n",
1777:        "      <td>0</td>\n",
1778:        "    </tr>\n",
1779:        "    <tr>\n",
1780:        "      <th>49877</th>\n",
1781:        "      <td>5</td>\n",
1782:        "      <td>yum</td>\n",
1783:        "      <td>1</td>\n",
1784:        "    </tr>\n",
1785:        "    <tr>\n",
1786:        "      <th>49961</th>\n",
1787:        "      <td>4</td>\n",
1788:        "      <td>nom</td>\n",
1789:        "      <td>1</td>\n",
1790:        "    </tr>\n",
1791:        "    <tr>\n",
1792:        "      <th>49996</th>\n",
1793:        "      <td>5</td>\n",
1794:        "      <td>looks good</td>\n",
1795:        "      <td>1</td>\n",
1796:        "    </tr>\n",
1797:        "  </tbody>\n",
1798:        "</table>\n",
1799:        "<p>570 rows × 3 columns</p>\n",
1800:        "</div>"
1801:       ],
1802:       "text/plain": [
1803:        "       rating             review  label\n",
1804:        "56          5     still the best      1\n",
1805:        "75          5    love this place      1\n",
1806:        "421         5                  5      1\n",
1807:        "854         5        great place      1\n",
1808:        "908         3  i like the drinks      1\n",
1809:        "...       ...                ...    ...\n",
1810:        "49848       5          excellent      1\n",
1811:        "49858       5            love it      0\n",
1812:        "49877       5                yum      1\n",
1813:        "49961       4                nom      1\n",
1814:        "49996       5         looks good      1\n",
1815:        "\n",
1816:        "[570 rows x 3 columns]"
1817:       ]
1818:      },
1819:      "execution_count": 544,
1820:      "metadata": {},
1821:      "output_type": "execute_result"
1822:     }
1823:    ],
1824:    "source": [
1825:     "# Print rows where text has fewer than 20 characters\n",
1826:     "yelp_sample[yelp_sample[\"review\"].str.len() < 20]"
1827:    ]
1828:   },
1829:   {
1830:    "cell_type": "code",
1831:    "execution_count": 545,
1832:    "id": "5bf7419d",
1833:    "metadata": {},
1834:    "outputs": [
1835:     {
1836:      "name": "stdout",
1837:      "output_type": "stream",
1838:      "text": [
1839:       "Label Distribution (Count):\n",
1840:       "label\n",
1841:       "0    117\n",
1842:       "1    453\n",
1843:       "Name: count, dtype: int64\n",
1844:       "\n",
1845:       "Label Distribution (Percentage):\n",
1846:       "label\n",
1847:       "0    20.53\n",
1848:       "1    79.47\n",
1849:       "Name: count, dtype: float64\n"
1850:      ]
1851:     }
1852:    ],
1853:    "source": [
1854:     "short_yelp_reviews = yelp_sample[yelp_sample[\"review\"].str.len() < 20]\n",
1855:     "\n",
1856:     "# Label counts\n",
1857:     "label_counts = short_yelp_reviews[\"label\"].value_counts().sort_index()\n",
1858:     "\n",
1859:     "print(\"Label Distribution (Count):\")\n",
1860:     "print(label_counts)\n",
1861:     "\n",
1862:     "print(\"\\nLabel Distribution (Percentage):\")\n",
1863:     "print((label_counts / len(short_yelp_reviews) * 100).round(2))"
1864:    ]
1865:   },
1866:   {
1867:    "cell_type": "code",
1868:    "execution_count": 546,
1869:    "id": "d3a4beb9",
1870:    "metadata": {},
1871:    "outputs": [
1872:     {
1873:      "data": {
1874:       "text/html": [
1875:        "<div>\n",
1876:        "<style scoped>\n",
1877:        "    .dataframe tbody tr th:only-of-type {\n",
1878:        "        vertical-align: middle;\n",
1879:        "    }\n",
1880:        "\n",
1881:        "    .dataframe tbody tr th {\n",
1882:        "        vertical-align: top;\n",
1883:        "    }\n",
1884:        "\n",
1885:        "    .dataframe thead th {\n",
1886:        "        text-align: right;\n",
1887:        "    }\n",
1888:        "</style>\n",
1889:        "<table border=\"1\" class=\"dataframe\">\n",
1890:        "  <thead>\n",
1891:        "    <tr style=\"text-align: right;\">\n",
1892:        "      <th></th>\n",
1893:        "      <th>rating</th>\n",
1894:        "      <th>review</th>\n",
1895:        "      <th>label</th>\n",
1896:        "      <th>review_length</th>\n",
1897:        "    </tr>\n",
1898:        "  </thead>\n",
1899:        "  <tbody>\n",
1900:        "    <tr>\n",
1901:        "      <th>48267</th>\n",
1902:        "      <td>5</td>\n",
1903:        "      <td>cheap and delicious</td>\n",
1904:        "      <td>1</td>\n",
1905:        "      <td>19</td>\n",
1906:        "    </tr>\n",
1907:        "    <tr>\n",
1908:        "      <th>47366</th>\n",
1909:        "      <td>5</td>\n",
1910:        "      <td>very very very good</td>\n",
1911:        "      <td>1</td>\n",
1912:        "      <td>19</td>\n",
1913:        "    </tr>\n",
1914:        "    <tr>\n",
1915:        "      <th>45673</th>\n",
1916:        "      <td>5</td>\n",
1917:        "      <td>great place love it</td>\n",
1918:        "      <td>1</td>\n",
1919:        "      <td>19</td>\n",
1920:        "    </tr>\n",
1921:        "    <tr>\n",
1922:        "      <th>2359</th>\n",
1923:        "      <td>3</td>\n",
1924:        "      <td>white sauce is good</td>\n",
1925:        "      <td>1</td>\n",
1926:        "      <td>19</td>\n",
1927:        "    </tr>\n",
1928:        "    <tr>\n",
1929:        "      <th>3039</th>\n",
1930:        "      <td>4</td>\n",
1931:        "      <td>i loved their tacos</td>\n",
1932:        "      <td>1</td>\n",
1933:        "      <td>19</td>\n",
1934:        "    </tr>\n",
1935:        "    <tr>\n",
1936:        "      <th>...</th>\n",
1937:        "      <td>...</td>\n",
1938:        "      <td>...</td>\n",
1939:        "      <td>...</td>\n",
1940:        "      <td>...</td>\n",
1941:        "    </tr>\n",
1942:        "    <tr>\n",
1943:        "      <th>40750</th>\n",
1944:        "      <td>5</td>\n",
1945:        "      <td>yum</td>\n",
1946:        "      <td>0</td>\n",
1947:        "      <td>3</td>\n",
1948:        "    </tr>\n",
1949:        "    <tr>\n",
1950:        "      <th>49961</th>\n",
1951:        "      <td>4</td>\n",
1952:        "      <td>nom</td>\n",
1953:        "      <td>1</td>\n",
1954:        "      <td>3</td>\n",
1955:        "    </tr>\n",
1956:        "    <tr>\n",
1957:        "      <th>44802</th>\n",
1958:        "      <td>5</td>\n",
1959:        "      <td>woo</td>\n",
1960:        "      <td>1</td>\n",
1961:        "      <td>3</td>\n",
1962:        "    </tr>\n",
1963:        "    <tr>\n",
1964:        "      <th>23950</th>\n",
1965:        "      <td>2</td>\n",
1966:        "      <td>ok</td>\n",
1967:        "      <td>1</td>\n",
1968:        "      <td>2</td>\n",
1969:        "    </tr>\n",
1970:        "    <tr>\n",
1971:        "      <th>421</th>\n",
1972:        "      <td>5</td>\n",
1973:        "      <td>5</td>\n",
1974:        "      <td>1</td>\n",
1975:        "      <td>1</td>\n",
1976:        "    </tr>\n",
1977:        "  </tbody>\n",
1978:        "</table>\n",
1979:        "<p>570 rows × 4 columns</p>\n",
1980:        "</div>"
1981:       ],
1982:       "text/plain": [
1983:        "       rating               review  label  review_length\n",
1984:        "48267       5  cheap and delicious      1             19\n",
1985:        "47366       5  very very very good      1             19\n",

(Output capped at 50 KB. Showing lines 501-1985. Use offset=1986 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 8.1s)

_Thinking:_

Let me continue reading the rest of the notebook to see all the markdown cells the user has added.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 1986,
  "limit": 2000
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
1986:        "45673       5  great place love it      1             19\n",
1987:        "2359        3  white sauce is good      1             19\n",
1988:        "3039        4  i loved their tacos      1             19\n",
1989:        "...       ...                  ...    ...            ...\n",
1990:        "40750       5                  yum      0              3\n",
1991:        "49961       4                  nom      1              3\n",
1992:        "44802       5                  woo      1              3\n",
1993:        "23950       2                   ok      1              2\n",
1994:        "421         5                    5      1              1\n",
1995:        "\n",
1996:        "[570 rows x 4 columns]"
1997:       ]
1998:      },
1999:      "execution_count": 546,
2000:      "metadata": {},
2001:      "output_type": "execute_result"
2002:     }
2003:    ],
2004:    "source": [
2005:     "yelp_sample[\n",
2006:     "    yelp_sample[\"review\"].str.len() < 20\n",
2007:     "].assign(\n",
2008:     "    review_length=yelp_sample[\"review\"].str.len()\n",
2009:     ").sort_values(\n",
2010:     "    by=\"review_length\", ascending=False\n",
2011:     ")"
2012:    ]
2013:   },
2014:   {
2015:    "cell_type": "code",
2016:    "execution_count": 547,
2017:    "id": "f96d07a5",
2018:    "metadata": {},
2019:    "outputs": [
2020:     {
2021:      "data": {
2022:       "text/html": [
2023:        "<div>\n",
2024:        "<style scoped>\n",
2025:        "    .dataframe tbody tr th:only-of-type {\n",
2026:        "        vertical-align: middle;\n",
2027:        "    }\n",
2028:        "\n",
2029:        "    .dataframe tbody tr th {\n",
2030:        "        vertical-align: top;\n",
2031:        "    }\n",
2032:        "\n",
2033:        "    .dataframe thead th {\n",
2034:        "        text-align: right;\n",
2035:        "    }\n",
2036:        "</style>\n",
2037:        "<table border=\"1\" class=\"dataframe\">\n",
2038:        "  <thead>\n",
2039:        "    <tr style=\"text-align: right;\">\n",
2040:        "      <th></th>\n",
2041:        "      <th>rating</th>\n",
2042:        "      <th>review</th>\n",
2043:        "      <th>label</th>\n",
2044:        "    </tr>\n",
2045:        "  </thead>\n",
2046:        "  <tbody>\n",
2047:        "    <tr>\n",
2048:        "      <th>1</th>\n",
2049:        "      <td>2</td>\n",
2050:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2051:        "      <td>0</td>\n",
2052:        "    </tr>\n",
2053:        "    <tr>\n",
2054:        "      <th>2</th>\n",
2055:        "      <td>3</td>\n",
2056:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2057:        "      <td>0</td>\n",
2058:        "    </tr>\n",
2059:        "    <tr>\n",
2060:        "      <th>3</th>\n",
2061:        "      <td>2</td>\n",
2062:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2063:        "      <td>0</td>\n",
2064:        "    </tr>\n",
2065:        "    <tr>\n",
2066:        "      <th>5</th>\n",
2067:        "      <td>1</td>\n",
2068:        "      <td>i went to this restaurant last saturday based on the reviews that my friend saw on yelp well i can easily say that this is the worst food i have ever eaten at a restaurant i have no idea what thos...</td>\n",
2069:        "      <td>1</td>\n",
2070:        "    </tr>\n",
2071:        "    <tr>\n",
2072:        "      <th>6</th>\n",
2073:        "      <td>4</td>\n",
2074:        "      <td>place was nice looking staff were friendly and food was delicious we were seated in the main dining area as there were no seats available in the back yard a c was pumping and place was a bit chill...</td>\n",
2075:        "      <td>0</td>\n",
2076:        "    </tr>\n",
2077:        "    <tr>\n",
2078:        "      <th>...</th>\n",
2079:        "      <td>...</td>\n",
2080:        "      <td>...</td>\n",
2081:        "      <td>...</td>\n",
2082:        "    </tr>\n",
2083:        "    <tr>\n",
2084:        "      <th>49988</th>\n",
2085:        "      <td>3</td>\n",
2086:        "      <td>good very inexpensive basic cantonese food you can even eat healthy here if you are careful about what you order more of a lunch place than dinner if you care about cleanliness you will mind the s...</td>\n",
2087:        "      <td>0</td>\n",
2088:        "    </tr>\n",
2089:        "    <tr>\n",
2090:        "      <th>49989</th>\n",
2091:        "      <td>2</td>\n",
2092:        "      <td>david chang you may be slightly overrated went with a group of six we ordered 1 the kimchee w pears 2 hamachi 3 oysters w kimchee foam 4 the pork buns and of course 5 the pork shoulder the best by...</td>\n",
2093:        "      <td>1</td>\n",
2094:        "    </tr>\n",
2095:        "    <tr>\n",
2096:        "      <th>49990</th>\n",
2097:        "      <td>5</td>\n",
2098:        "      <td>first went to soco a few weeks before the grand opening the grand opening was in late july so im guessing late june is when i first went they were only open sporadically then and they were testing...</td>\n",
2099:        "      <td>1</td>\n",
2100:        "    </tr>\n",
2101:        "    <tr>\n",
2102:        "      <th>49992</th>\n",
2103:        "      <td>5</td>\n",
2104:        "      <td>a friend was in town and i learned this was her spot the must do thing on the line up having never been sounded good to me everything was under complete control here you walked in and you either h...</td>\n",
2105:        "      <td>1</td>\n",
2106:        "    </tr>\n",
2107:        "    <tr>\n",
2108:        "      <th>49998</th>\n",
2109:        "      <td>5</td>\n",
2110:        "      <td>laissez les bons temps rouler who on earth would ever guess that this place would be on satan s island if it weren t for the b f living here i wouldn t visit or pay the toll but for bayou i would ...</td>\n",
2111:        "      <td>0</td>\n",
2112:        "    </tr>\n",
2113:        "  </tbody>\n",
2114:        "</table>\n",
2115:        "<p>18962 rows × 3 columns</p>\n",
2116:        "</div>"
2117:       ],
2118:       "text/plain": [
2119:        "       rating  \\\n",
2120:        "1           2   \n",
2121:        "2           3   \n",
2122:        "3           2   \n",
2123:        "5           1   \n",
2124:        "6           4   \n",
2125:        "...       ...   \n",
2126:        "49988       3   \n",
2127:        "49989       2   \n",
2128:        "49990       5   \n",
2129:        "49992       5   \n",
2130:        "49998       5   \n",
2131:        "\n",
2132:        "                                                                                                                                                                                                        review  \\\n",
2133:        "1      the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2134:        "2      very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2135:        "3      i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2136:        "5      i went to this restaurant last saturday based on the reviews that my friend saw on yelp well i can easily say that this is the worst food i have ever eaten at a restaurant i have no idea what thos...   \n",
2137:        "6      place was nice looking staff were friendly and food was delicious we were seated in the main dining area as there were no seats available in the back yard a c was pumping and place was a bit chill...   \n",
2138:        "...                                                                                                                                                                                                        ...   \n",
2139:        "49988  good very inexpensive basic cantonese food you can even eat healthy here if you are careful about what you order more of a lunch place than dinner if you care about cleanliness you will mind the s...   \n",
2140:        "49989  david chang you may be slightly overrated went with a group of six we ordered 1 the kimchee w pears 2 hamachi 3 oysters w kimchee foam 4 the pork buns and of course 5 the pork shoulder the best by...   \n",
2141:        "49990  first went to soco a few weeks before the grand opening the grand opening was in late july so im guessing late june is when i first went they were only open sporadically then and they were testing...   \n",
2142:        "49992  a friend was in town and i learned this was her spot the must do thing on the line up having never been sounded good to me everything was under complete control here you walked in and you either h...   \n",
2143:        "49998  laissez les bons temps rouler who on earth would ever guess that this place would be on satan s island if it weren t for the b f living here i wouldn t visit or pay the toll but for bayou i would ...   \n",
2144:        "\n",
2145:        "       label  \n",
2146:        "1          0  \n",
2147:        "2          0  \n",
2148:        "3          0  \n",
2149:        "5          1  \n",
2150:        "6          0  \n",
2151:        "...      ...  \n",
2152:        "49988      0  \n",
2153:        "49989      1  \n",
2154:        "49990      1  \n",
2155:        "49992      1  \n",
2156:        "49998      0  \n",
2157:        "\n",
2158:        "[18962 rows x 3 columns]"
2159:       ]
2160:      },
2161:      "execution_count": 547,
2162:      "metadata": {},
2163:      "output_type": "execute_result"
2164:     }
2165:    ],
2166:    "source": [
2167:     "yelp_sample[yelp_sample[\"review\"].str.len() > 500]"
2168:    ]
2169:   },
2170:   {
2171:    "cell_type": "markdown",
2172:    "id": "86a3f1c5",
2173:    "metadata": {},
2174:    "source": [
2175:     "When detecting AI-generated reviews, very short texts provide insufficient linguistic signal to reliably distinguish between human and AI."
2176:    ]
2177:   },
2178:   {
2179:    "cell_type": "code",
2180:    "execution_count": 548,
2181:    "id": "f1b0f41e",
2182:    "metadata": {},
2183:    "outputs": [],
2184:    "source": [
2185:     "yelp_sample = yelp_sample[yelp_sample[\"review\"].str.len() >= 20]"
2186:    ]
2187:   },
2188:   {
2189:    "cell_type": "code",
2190:    "execution_count": 549,
2191:    "id": "49439f21",
2192:    "metadata": {},
2193:    "outputs": [],
2194:    "source": [
2195:     "amazon_df=amazon_df[amazon_df[\"review\"].str.len() >= 20]"
2196:    ]
2197:   },
2198:   {
2199:    "cell_type": "code",
2200:    "execution_count": 550,
2201:    "id": "e54669f8",
2202:    "metadata": {},
2203:    "outputs": [
2204:     {
2205:      "name": "stdout",
2206:      "output_type": "stream",
2207:      "text": [
2208:       "Empty Reviews : 0\n",
2209:       "Average Review Length : 535.9302043293546\n",
2210:       "Shortest Review Length : 20\n",
2211:       "Longest Review Length : 4907\n"
2212:      ]
2213:     }
2214:    ],
2215:    "source": [
2216:     "#yelp\n",
2217:     "\n",
2218:     "print(\"Empty Reviews :\", (yelp_sample[\"review\"] == \"\").sum())\n",
2219:     "\n",
2220:     "print(\"Average Review Length :\", yelp_sample[\"review\"].str.len().mean())\n",
2221:     "\n",
2222:     "print(\"Shortest Review Length :\", yelp_sample[\"review\"].str.len().min())\n",
2223:     "\n",
2224:     "print(\"Longest Review Length :\", yelp_sample[\"review\"].str.len().max())"
2225:    ]
2226:   },
2227:   {
2228:    "cell_type": "code",
2229:    "execution_count": 551,
2230:    "id": "a1ac3c21",
2231:    "metadata": {},
2232:    "outputs": [
2233:     {
2234:      "name": "stdout",
2235:      "output_type": "stream",
2236:      "text": [
2237:       "Empty Reviews : 0\n",
2238:       "Average Review Length : 339.9354319796075\n",
2239:       "Shortest Review Length : 24\n",
2240:       "Longest Review Length : 2095\n"
2241:      ]
2242:     }
2243:    ],
2244:    "source": [
2245:     "#amazon\n",
2246:     "\n",
2247:     "print(\"Empty Reviews :\", (amazon_df[\"review\"] == \"\").sum())\n",
2248:     "\n",
2249:     "print(\"Average Review Length :\", amazon_df[\"review\"].str.len().mean())\n",
2250:     "\n",
2251:     "print(\"Shortest Review Length :\", amazon_df[\"review\"].str.len().min())\n",
2252:     "\n",
2253:     "print(\"Longest Review Length :\", amazon_df[\"review\"].str.len().max())"
2254:    ]
2255:   },
2256:   {
2257:    "cell_type": "markdown",
2258:    "id": "afeac13d",
2259:    "metadata": {},
2260:    "source": [
2261:     "### Exploratory Data Analysis"
2262:    ]
2263:   },
2264:   {
2265:    "cell_type": "code",
2266:    "execution_count": 552,
2267:    "id": "fa86f547",
2268:    "metadata": {},
2269:    "outputs": [
2270:     {
2271:      "name": "stderr",
2272:      "output_type": "stream",
2273:      "text": [
2274:       "/opt/python-venvs/work/lib/python3.12/site-packages/nltk/downloader.py:1076: UserWarning: NLTK will not authorize the non-private download directory '/home/hitesh/nltk_data': it (or an ancestor) is world- or group-writable, so another local user could plant files there. Choose a private location such as ~/nltk_data.\n",
2275:       "  for msg in self.incr_download(info_or_id, download_dir, force):\n",
2276:       "[nltk_data] Downloading package punkt to /home/hitesh/nltk_data...\n",
2277:       "[nltk_data]   Package punkt is already up-to-date!\n",
2278:       "[nltk_data] Downloading package punkt_tab to /home/hitesh/nltk_data...\n",
2279:       "[nltk_data]   Package punkt_tab is already up-to-date!\n"
2280:      ]
2281:     },
2282:     {
2283:      "data": {
2284:       "text/plain": [
2285:        "True"
2286:       ]
2287:      },
2288:      "execution_count": 552,
2289:      "metadata": {},
2290:      "output_type": "execute_result"
2291:     }
2292:    ],
2293:    "source": [
2294:     "import matplotlib.pyplot as plt\n",
2295:     "from wordcloud import WordCloud\n",
2296:     "from collections import Counter\n",
2297:     "from sklearn.feature_extraction.text import CountVectorizer\n",
2298:     "import nltk\n",
2299:     "\n",
2300:     "nltk.download(\"punkt\")\n",
2301:     "nltk.download(\"punkt_tab\")"
2302:    ]
2303:   },
2304:   {
2305:    "cell_type": "code",
2306:    "execution_count": 553,
2307:    "id": "3a88a628",
2308:    "metadata": {},
2309:    "outputs": [
2310:     {
2311:      "name": "stdout",
2312:      "output_type": "stream",
2313:      "text": [
2314:       "Dataset Shape : (40407, 3)\n",
2315:       "\n",
2316:       "Class Distribution:\n",
2317:       "\n",
2318:       "label\n",
2319:       "0    20215\n",
2320:       "1    20192\n",
2321:       "Name: count, dtype: int64\n"
2322:      ]
2323:     },
2324:     {
2325:      "data": {
2326:       "text/html": [
2327:        "<div>\n",
2328:        "<style scoped>\n",
2329:        "    .dataframe tbody tr th:only-of-type {\n",
2330:        "        vertical-align: middle;\n",
2331:        "    }\n",
2332:        "\n",
2333:        "    .dataframe tbody tr th {\n",
2334:        "        vertical-align: top;\n",
2335:        "    }\n",
2336:        "\n",
2337:        "    .dataframe thead th {\n",
2338:        "        text-align: right;\n",
2339:        "    }\n",
2340:        "</style>\n",
2341:        "<table border=\"1\" class=\"dataframe\">\n",
2342:        "  <thead>\n",
2343:        "    <tr style=\"text-align: right;\">\n",
2344:        "      <th></th>\n",
2345:        "      <th>rating</th>\n",
2346:        "      <th>review</th>\n",
2347:        "      <th>label</th>\n",
2348:        "    </tr>\n",
2349:        "  </thead>\n",
2350:        "  <tbody>\n",
2351:        "    <tr>\n",
2352:        "      <th>0</th>\n",
2353:        "      <td>5</td>\n",
2354:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2355:        "      <td>1</td>\n",
2356:        "    </tr>\n",
2357:        "    <tr>\n",
2358:        "      <th>1</th>\n",
2359:        "      <td>5</td>\n",
2360:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2361:        "      <td>1</td>\n",
2362:        "    </tr>\n",
2363:        "    <tr>\n",
2364:        "      <th>2</th>\n",
2365:        "      <td>5</td>\n",
2366:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2367:        "      <td>1</td>\n",
2368:        "    </tr>\n",
2369:        "    <tr>\n",
2370:        "      <th>3</th>\n",
2371:        "      <td>1</td>\n",
2372:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2373:        "      <td>1</td>\n",
2374:        "    </tr>\n",
2375:        "    <tr>\n",
2376:        "      <th>4</th>\n",
2377:        "      <td>5</td>\n",
2378:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2379:        "      <td>1</td>\n",
2380:        "    </tr>\n",
2381:        "  </tbody>\n",
2382:        "</table>\n",
2383:        "</div>"
2384:       ],
2385:       "text/plain": [
2386:        "   rating  \\\n",
2387:        "0       5   \n",
2388:        "1       5   \n",
2389:        "2       5   \n",
2390:        "3       1   \n",
2391:        "4       5   \n",
2392:        "\n",
2393:        "                                                                                review  \\\n",
2394:        "0                love this well made sturdy and very comfortable i love it very pretty   \n",
2395:        "1        love it a great upgrade from the original i ve had mine for a couple of years   \n",
2396:        "2                    this pillow saved my back i love the look and feel of this pillow   \n",
2397:        "3       missing information on how to use it but it is a great product for the price i   \n",
2398:        "4  very nice set good quality we have had the set for two months now and have not been   \n",
2399:        "\n",
2400:        "   label  \n",
2401:        "0      1  \n",
2402:        "1      1  \n",
2403:        "2      1  \n",
2404:        "3      1  \n",
2405:        "4      1  "
2406:       ]
2407:      },
2408:      "execution_count": 553,
2409:      "metadata": {},
2410:      "output_type": "execute_result"
2411:     }
2412:    ],
2413:    "source": [
2414:     "#amazon\n",
2415:     "\n",
2416:     "print(\"Dataset Shape :\", amazon_df.shape)\n",
2417:     "print(\"\\nClass Distribution:\\n\")\n",
2418:     "print(amazon_df[\"label\"].value_counts())\n",
2419:     "\n",
2420:     "amazon_df.head()"
2421:    ]
2422:   },
2423:   {
2424:    "cell_type": "code",
2425:    "execution_count": 554,
2426:    "id": "b98ee1c0",
2427:    "metadata": {},
2428:    "outputs": [
2429:     {
2430:      "name": "stdout",
2431:      "output_type": "stream",
2432:      "text": [
2433:       "Dataset Shape : (49430, 3)\n",
2434:       "\n",
2435:       "Class Distribution:\n",
2436:       "\n",
2437:       "label\n",
2438:       "0    24883\n",
2439:       "1    24547\n",
2440:       "Name: count, dtype: int64\n"
2441:      ]
2442:     },
2443:     {
2444:      "data": {
2445:       "text/html": [
2446:        "<div>\n",
2447:        "<style scoped>\n",
2448:        "    .dataframe tbody tr th:only-of-type {\n",
2449:        "        vertical-align: middle;\n",
2450:        "    }\n",
2451:        "\n",
2452:        "    .dataframe tbody tr th {\n",
2453:        "        vertical-align: top;\n",
2454:        "    }\n",
2455:        "\n",
2456:        "    .dataframe thead th {\n",
2457:        "        text-align: right;\n",
2458:        "    }\n",
2459:        "</style>\n",
2460:        "<table border=\"1\" class=\"dataframe\">\n",
2461:        "  <thead>\n",
2462:        "    <tr style=\"text-align: right;\">\n",
2463:        "      <th></th>\n",
2464:        "      <th>rating</th>\n",
2465:        "      <th>review</th>\n",
2466:        "      <th>label</th>\n",
2467:        "    </tr>\n",
2468:        "  </thead>\n",
2469:        "  <tbody>\n",
2470:        "    <tr>\n",
2471:        "      <th>0</th>\n",
2472:        "      <td>5</td>\n",
2473:        "      <td>my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...</td>\n",
2474:        "      <td>1</td>\n",
2475:        "    </tr>\n",
2476:        "    <tr>\n",
2477:        "      <th>1</th>\n",
2478:        "      <td>2</td>\n",
2479:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2480:        "      <td>0</td>\n",
2481:        "    </tr>\n",
2482:        "    <tr>\n",
2483:        "      <th>2</th>\n",
2484:        "      <td>3</td>\n",
2485:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2486:        "      <td>0</td>\n",
2487:        "    </tr>\n",
2488:        "    <tr>\n",
2489:        "      <th>3</th>\n",
2490:        "      <td>2</td>\n",
2491:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2492:        "      <td>0</td>\n",
2493:        "    </tr>\n",
2494:        "    <tr>\n",
2495:        "      <th>4</th>\n",
2496:        "      <td>5</td>\n",
2497:        "      <td>my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried</td>\n",
2498:        "      <td>1</td>\n",
2499:        "    </tr>\n",
2500:        "  </tbody>\n",
2501:        "</table>\n",
2502:        "</div>"
2503:       ],
2504:       "text/plain": [
2505:        "   rating  \\\n",
2506:        "0       5   \n",
2507:        "1       2   \n",
2508:        "2       3   \n",
2509:        "3       2   \n",
2510:        "4       5   \n",
2511:        "\n",
2512:        "                                                                                                                                                                                                    review  \\\n",
2513:        "0  my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...   \n",
2514:        "1  the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2515:        "2  very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2516:        "3  i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2517:        "4                                                my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried   \n",
2518:        "\n",
2519:        "   label  \n",
2520:        "0      1  \n",
2521:        "1      0  \n",
2522:        "2      0  \n",
2523:        "3      0  \n",
2524:        "4      1  "
2525:       ]
2526:      },
2527:      "execution_count": 554,
2528:      "metadata": {},
2529:      "output_type": "execute_result"
2530:     }
2531:    ],
2532:    "source": [
2533:     "#Yelp\n",
2534:     "\n",
2535:     "print(\"Dataset Shape :\", yelp_sample.shape)\n",
2536:     "print(\"\\nClass Distribution:\\n\")\n",
2537:     "print(yelp_sample[\"label\"].value_counts())\n",
2538:     "\n",
2539:     "yelp_sample.head()"
2540:    ]
2541:   },
2542:   {
2543:    "cell_type": "code",
2544:    "execution_count": 586,
2545:    "id": "c94a51a5",
2546:    "metadata": {},
2547:    "outputs": [
2548:     {
2549:      "data": {
2550:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAi8AAAF1CAYAAAAgKQpIAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUMhJREFUeJzt3XdYFNf6B/Av0kSQZsGGQMQSu1hQEUEpFuxiNIolAkZjTKyJJWo015ZyjRpvLCAxGjX2WGJDxY7KtYtdKTakyKKCSzu/P7zMz3EBl3VhWfP9PM8+T/bMO2fe3XvHfTlz5oyBEEKAiIiISE+U0XUCREREREXB4oWIiIj0CosXIiIi0issXoiIiEivsHghIiIivcLihYiIiPQKixciIiLSKyxeiIiISK+weCF6zfXr1xESEoL09HSdHe/SpUsICQlBZmZmieRQUB6l1Y0bN7Bx40aEhIQgPj5e1+mQhhQKBUJCQnDnzh1dp0J6yEjXCRAVl7t37+LQoUPSexMTE1hZWaFOnTqoW7cuypRRrd0jIiIwatQodO7cGeXKlVP7WFevXsWpU6cwaNAgmJmZqb1ffsf7+++/MWXKFPj7+8PExETtvt4lR00/d0n78ccfMX36dHTv3h2WlpZo1aoV7O3tC90nISEBO3fuhK2tLfr06VNCmeqHN88RQ0NDVKhQAa6urrCzsyvWYz969AjBwcFYs2YNatWqVazHovcPixd6b505cwbBwcHw8vKCo6MjcnJykJSUhKioKADAqFGj8PXXX8PU1FTa58MPP0RgYCDMzc2LdKwDBw5g3Lhx6NatW5GKF02Pp4nCcizJPDSVlZWFGTNmYNy4cZg7d67a+y1duhTfffcdDA0NERMTgxo1ahRjlvrlzXMkMzMTFy9exNWrVzFhwgQsWLCg2I5tbW2NwMBAODs7F9sx6P3F4oXeeyNHjoS/v7/0Pjc3F2vWrMGoUaNw6NAh7N+/Xxrh8PDwgIeHR4nlVtLHK+15FCY+Ph4ZGRlF+is9JycHYWFh6N69Ow4cOICwsDBMnz69GLPUT6+fI0IIjBw5Et9//z3atGmDXr16Fcsxq1SpgpCQkGLpm95/LF7oH6dMmTIYOnQo0tPT8dlnn+E///kPxo4dC+DV3I/jx49j4MCBsssnz58/x8mTJ5GYmIiaNWuiRYsW0uhFZGQkIiMjAQDr1q2DpaUlAMDPzw9Vq1bFpUuXcObMGQwZMgTZ2dk4ePAgkpOTMWzYsAKPl+fZs2cIDw9HZmYm2rdvj6pVq8q2nzp1Cjdv3sTQoUNl7bGxsThw4AB69uyJSpUqvTXHwvJ48OABTp06hZcvX6Ju3bpo0aIFDAwMpO1vfr4DBw4gPT0d7u7uRRrlKOw4R48eRUREBADgxIkTEELA3NwcH3/8caF97t27F/fv38fmzZtha2uL0NBQTJs2TeWS4eufQalUIjw8HADg6+srjUY9e/YMhw4dglKphJeXFypUqJDvdw4ABgYGKFeuHBo0aIDGjRtLMUqlEmvWrCkw3759+8LGxkat7+TNvN/lu3+dgYEBPv30U6xYsQL79u1TKV6ysrJw6tQpxMbGwsrKCu7u7lLOycnJ2LZtG9q0aYMGDRqo9L1u3TpUrFgRvr6+UCgU2LRpEzp06KBSkBZ2DCEEwsLC0LhxY7Ro0ULaZ+fOnUhISMBHH30k/f87NTUVmzdvhqenpzTCk5ubi1OnTiEuLg62trZwcXFBpUqVNPquSIcE0Xtq/fr1AoDYtGlTvttfvnwpzM3NhYuLi9T266+/CgAiPj5eatuxY4ewsrISzZs3FwEBAaJDhw6idu3aYv/+/UIIITZs2CBat24tAIiBAweKwMBAERgYKK5fvy6EEGLevHkCgDh06JBo0qSJ6NOnj3B0dCzweHnx4eHholGjRsLf3180bdpUmJqaimXLlsk+w+jRo4W5ubnKZ9u2bZsAIE6dOqVWjvnlkZubKyZM... (line truncated to 2000 chars)
2551:       "text/plain": [
2552:        "<Figure size 600x400 with 1 Axes>"
2553:       ]
2554:      },
2555:      "metadata": {},
2556:      "output_type": "display_data"
2557:     }
2558:    ],
2559:    "source": [
2560:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
2561:     "\n",
2562:     "plt.figure(figsize=(6,4))\n",
2563:     "plt.bar([\"Genuine (0)\", \"AI Generated (1)\"], label_counts.values)\n",
2564:     "plt.title(\"Distribution of Amazon Reviews\")\n",
2565:     "plt.ylabel(\"Number of Reviews\")\n",
2566:     "\n",
2567:     "for i, value in enumerate(label_counts.values):\n",
2568:     "    plt.text(i, value, str(value), ha=\"center\", va=\"bottom\")\n",
2569:     "\n",
2570:     "plt.show()"
2571:    ]
2572:   },
2573:   {
2574:    "cell_type": "code",
2575:    "execution_count": 587,
2576:    "id": "c8e7b73f",
2577:    "metadata": {},
2578:    "outputs": [
2579:     {
2580:      "data": {
2581:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAi8AAAF1CAYAAAAgKQpIAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAR3VJREFUeJzt3XdYFNf+BvAX6UWwYUdQsATFghURpaPYBaNeNcbeNTHxqkksGCOa5k2MNxp7LLH3xB7RxIIYwKhY0KhgCUGRRaXD+f3hZX6MS1nWhWX0/TzPPE/2zJkz312zuy+zZ2YMhBACRERERApRQd8FEBEREZUEwwsREREpCsMLERERKQrDCxERESkKwwsREREpCsMLERERKQrDCxERESkKwwsREREpCsMLUSnYu3cvDh8+rNf9bd++HcePHy+zGgqrozzKzs5GWFgY1q1bh82bN5fqvoQQWLVqFSIjI0t1P2XpwIED+Pnnn/VdBr3BDHiFXaKiHTx4EPfv3wcAGBgYwNLSEra2tnBxcUH16tUL3KZNmzaoVq0aDh06VKJ97dq1C1ZWVvD39y/RdgXtz8nJCS1btsSOHTtKNNar1Kjt8y5L6enpcHd3R3JyMjp37owqVargq6++kvWJi4vDkSNH0Lp1a7Rq1arAcTZt2gQjIyMMGDCgyP1lZ2fD2NgYc+fOxbx583T1NLB+/XpkZWUBePH/pYWFBZo0aVJovbrUqVMnGBkZISwsrNT3RVQQI30XQFTeffXVV/jtt98wdOhQAEBaWhri4uJw4cIFuLq6IiQkBL6+vrJt+vTpAysrqxLva86cOXBwcChxeNF2f9ooqsayrENbW7ZsQWRkJG7duoUGDRoU2KdWrVpYvnw5Hjx4gEuXLqFq1aqy9T/88APGjh2LlStXlkXJBZo4cSIqV66MgIAAAMCDBw9w7NgxNG/eHLt374adnV2p7btnz56oUIEH7kmPBBEVycfHR9jY2Ki1//PPP2LgwIECgFi1apVO9tW0aVPRvXt3nYzl6OgogoKCdDJWfrqsUR9mzZolKlSoIHJzc4vsd/XqVWFubq72Gt68eVNYWVmJXr16abS/rKwsAUDMnTtX25ILZGlpKQICAmRtZ86cERUqVFD0vw+RJnjkhUhLtra22LhxI27duoUpU6agR48eqFGjBoAXcz/MzMykv4rzxMbG4vLly8jOzkbTpk3h7OwsrVu/fj2ePHkCQ0NDrFq1CgBgY2OD/v37A3gxh6VKlSrw8fHBzZs3ERERAQcHB7i5uRW6vzxXr15FZGQkqlevji5dusDExES2ft26dWjSpAk6dOggaz9y5AiePXuGfv36aVRjYXUIIXD+/HnExsbCwsICbm5uqFWrlqzPy8/v/PnzqFKlCry8vGBqalrMv0bx+xFCYPXq1YiIiAAArF69GgDg6uoKV1dXtbGaNGmCxYsXY8qUKVi/fj2GDRuGnJwcvPPOO7CwsJCevxACERERiI2NhampKdzd3dWe28syMjKwYcMGtG/fHi4uLjhz5gz++usvODk5qf0blISbmxtatGiBo0ePQggBAwMD2fqbN28iMjISWVlZaNmyJZo2bSqt27NnD3Jzc6V/6/z++OMPREVFYfDgwTA3N8eBAwdgYGCA7t27q/Utah+///477t69i8GDB0ttN27cwKlTp9CiRQu0bdtWat+/fz8qVKgg28etW7dw6dIlZGZmwtnZGc2aNdPuhSLl02t0IlKAwo685Fm3bp0AIP773/9Kba1bt5b9VZybmyuGDRsmLCwsRI8ePcTAgQOFi4uL8PPzEykpKUIIISZOnCgqV64s7OzsxMiRI8XIkSPFrFmzpDHyjqTMmzdPtG3bVvTo0UNMnTq1wP3l7//JJ5+Idu3aiaCgIGFraysaNWokbt26JetramoqjZVf9+7dRdOmTaXHxdVYUB23b98WrVq1ElWqVBF9+/YV7u7uwtjYWLZd/noXL14s... (line truncated to 2000 chars)
2582:       "text/plain": [
2583:        "<Figure size 600x400 with 1 Axes>"
2584:       ]
2585:      },
2586:      "metadata": {},
2587:      "output_type": "display_data"
2588:     }
2589:    ],
2590:    "source": [
2591:     "label_counts = yelp_sample[\"label\"].value_counts().sort_index()\n",
2592:     "\n",
2593:     "plt.figure(figsize=(6,4))\n",
2594:     "plt.bar([\"Genuine (0)\", \"AI Generated (1)\"], label_counts.values,color=\"red\")\n",
2595:     "plt.title(\"Distribution of Yelp Reviews\")\n",
2596:     "plt.ylabel(\"Number of Reviews\")\n",
2597:     "\n",
2598:     "for i, value in enumerate(label_counts.values):\n",
2599:     "    plt.text(i, value, str(value), ha=\"center\", va=\"bottom\")\n",
2600:     "\n",
2601:     "plt.show()"
2602:    ]
2603:   },
2604:   {
2605:    "cell_type": "markdown",
2606:    "id": "3d85db35",
2607:    "metadata": {},
2608:    "source": [
2609:     "### Feature Engineering"
2610:    ]
2611:   },
2612:   {
2613:    "cell_type": "markdown",
2614:    "id": "d5e65f85",
2615:    "metadata": {},
2616:    "source": [
2617:     "list the features being created: text_length, word_count, sentence_count, vocab_richness, avg_word_len"
2618:    ]
2619:   },
2620:   {
2621:    "cell_type": "code",
2622:    "execution_count": 557,
2623:    "id": "37794fd1",
2624:    "metadata": {},
2625:    "outputs": [
2626:     {
2627:      "data": {
2628:       "text/html": [
2629:        "<div>\n",
2630:        "<style scoped>\n",
2631:        "    .dataframe tbody tr th:only-of-type {\n",
2632:        "        vertical-align: middle;\n",
2633:        "    }\n",
2634:        "\n",
2635:        "    .dataframe tbody tr th {\n",
2636:        "        vertical-align: top;\n",
2637:        "    }\n",
2638:        "\n",
2639:        "    .dataframe thead th {\n",
2640:        "        text-align: right;\n",
2641:        "    }\n",
2642:        "</style>\n",
2643:        "<table border=\"1\" class=\"dataframe\">\n",
2644:        "  <thead>\n",
2645:        "    <tr style=\"text-align: right;\">\n",
2646:        "      <th></th>\n",
2647:        "      <th>review</th>\n",
2648:        "      <th>text_length</th>\n",
2649:        "      <th>word_count</th>\n",
2650:        "      <th>sentence_count</th>\n",
2651:        "    </tr>\n",
2652:        "  </thead>\n",
2653:        "  <tbody>\n",
2654:        "    <tr>\n",
2655:        "      <th>0</th>\n",
2656:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2657:        "      <td>69</td>\n",
2658:        "      <td>13</td>\n",
2659:        "      <td>1</td>\n",
2660:        "    </tr>\n",
2661:        "    <tr>\n",
2662:        "      <th>1</th>\n",
2663:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2664:        "      <td>77</td>\n",
2665:        "      <td>17</td>\n",
2666:        "      <td>1</td>\n",
2667:        "    </tr>\n",
2668:        "    <tr>\n",
2669:        "      <th>2</th>\n",
2670:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2671:        "      <td>65</td>\n",
2672:        "      <td>14</td>\n",
2673:        "      <td>1</td>\n",
2674:        "    </tr>\n",
2675:        "    <tr>\n",
2676:        "      <th>3</th>\n",
2677:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2678:        "      <td>78</td>\n",
2679:        "      <td>17</td>\n",
2680:        "      <td>1</td>\n",
2681:        "    </tr>\n",
2682:        "    <tr>\n",
2683:        "      <th>4</th>\n",
2684:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2685:        "      <td>83</td>\n",
2686:        "      <td>18</td>\n",
2687:        "      <td>1</td>\n",
2688:        "    </tr>\n",
2689:        "  </tbody>\n",
2690:        "</table>\n",
2691:        "</div>"
2692:       ],
2693:       "text/plain": [
2694:        "                                                                                review  \\\n",
2695:        "0                love this well made sturdy and very comfortable i love it very pretty   \n",
2696:        "1        love it a great upgrade from the original i ve had mine for a couple of years   \n",
2697:        "2                    this pillow saved my back i love the look and feel of this pillow   \n",
2698:        "3       missing information on how to use it but it is a great product for the price i   \n",
2699:        "4  very nice set good quality we have had the set for two months now and have not been   \n",
2700:        "\n",
2701:        "   text_length  word_count  sentence_count  \n",
2702:        "0           69          13               1  \n",
2703:        "1           77          17               1  \n",
2704:        "2           65          14               1  \n",
2705:        "3           78          17               1  \n",
2706:        "4           83          18               1  "
2707:       ]
2708:      },
2709:      "execution_count": 557,
2710:      "metadata": {},
2711:      "output_type": "execute_result"
2712:     }
2713:    ],
2714:    "source": [
2715:     "#feature engineering for amazon\n",
2716:     "\n",
2717:     "amazon_df[\"text_length\"] = amazon_df[\"review\"].str.len()\n",
2718:     "\n",
2719:     "amazon_df[\"word_count\"] = amazon_df[\"review\"].str.split().apply(len)\n",
2720:     "\n",
2721:     "amazon_df[\"sentence_count\"] = amazon_df[\"review\"].apply(\n",
2722:     "    lambda x: len([s for s in nltk.sent_tokenize(x) if s.strip()])\n",
2723:     ")\n",
2724:     "\n",
2725:     "amazon_df[[\"review\",\"text_length\", \"word_count\", \"sentence_count\"]].head()"
2726:    ]
2727:   },
2728:   {
2729:    "cell_type": "code",
2730:    "execution_count": 558,
2731:    "id": "6080e6ea",
2732:    "metadata": {},
2733:    "outputs": [
2734:     {
2735:      "data": {
2736:       "text/html": [
2737:        "<div>\n",
2738:        "<style scoped>\n",
2739:        "    .dataframe tbody tr th:only-of-type {\n",
2740:        "        vertical-align: middle;\n",
2741:        "    }\n",
2742:        "\n",
2743:        "    .dataframe tbody tr th {\n",
2744:        "        vertical-align: top;\n",
2745:        "    }\n",
2746:        "\n",
2747:        "    .dataframe thead th {\n",
2748:        "        text-align: right;\n",
2749:        "    }\n",
2750:        "</style>\n",
2751:        "<table border=\"1\" class=\"dataframe\">\n",
2752:        "  <thead>\n",
2753:        "    <tr style=\"text-align: right;\">\n",
2754:        "      <th></th>\n",
2755:        "      <th>review</th>\n",
2756:        "      <th>text_length</th>\n",
2757:        "      <th>word_count</th>\n",
2758:        "      <th>sentence_count</th>\n",
2759:        "    </tr>\n",
2760:        "  </thead>\n",
2761:        "  <tbody>\n",
2762:        "    <tr>\n",
2763:        "      <th>0</th>\n",
2764:        "      <td>my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...</td>\n",
2765:        "      <td>204</td>\n",
2766:        "      <td>40</td>\n",
2767:        "      <td>1</td>\n",
2768:        "    </tr>\n",
2769:        "    <tr>\n",
2770:        "      <th>1</th>\n",
2771:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2772:        "      <td>889</td>\n",
2773:        "      <td>169</td>\n",
2774:        "      <td>1</td>\n",
2775:        "    </tr>\n",
2776:        "    <tr>\n",
2777:        "      <th>2</th>\n",
2778:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2779:        "      <td>522</td>\n",
2780:        "      <td>107</td>\n",
2781:        "      <td>1</td>\n",
2782:        "    </tr>\n",
2783:        "    <tr>\n",
2784:        "      <th>3</th>\n",
2785:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2786:        "      <td>2489</td>\n",
2787:        "      <td>487</td>\n",
2788:        "      <td>1</td>\n",
2789:        "    </tr>\n",
2790:        "    <tr>\n",
2791:        "      <th>4</th>\n",
2792:        "      <td>my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried</td>\n",
2793:        "      <td>153</td>\n",
2794:        "      <td>32</td>\n",
2795:        "      <td>1</td>\n",
2796:        "    </tr>\n",
2797:        "  </tbody>\n",
2798:        "</table>\n",
2799:        "</div>"
2800:       ],
2801:       "text/plain": [
2802:        "                                                                                                                                                                                                    review  \\\n",
2803:        "0  my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...   \n",
2804:        "1  the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2805:        "2  very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2806:        "3  i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2807:        "4                                                my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried   \n",
2808:        "\n",
2809:        "   text_length  word_count  sentence_count  \n",
2810:        "0          204          40               1  \n",
2811:        "1          889         169               1  \n",
2812:        "2          522         107               1  \n",
2813:        "3         2489         487               1  \n",
2814:        "4          153          32               1  "
2815:       ]
2816:      },
2817:      "execution_count": 558,
2818:      "metadata": {},
2819:      "output_type": "execute_result"
2820:     }
2821:    ],
2822:    "source": [
2823:     "#feature engineering for yelp\n",
2824:     "\n",
2825:     "yelp_sample[\"text_length\"] = yelp_sample[\"review\"].str.len()\n",
2826:     "\n",
2827:     "yelp_sample[\"word_count\"] = yelp_sample[\"review\"].str.split().apply(len)\n",
2828:     "\n",
2829:     "yelp_sample[\"sentence_count\"] = yelp_sample[\"review\"].apply(\n",
2830:     "    lambda x: len([s for s in nltk.sent_tokenize(x) if s.strip()])\n",
2831:     ")\n",
2832:     "\n",
2833:     "yelp_sample[[\"review\",\"text_length\", \"word_count\", \"sentence_count\"]].head()"
2834:    ]
2835:   },
2836:   {
2837:    "cell_type": "markdown",
2838:    "id": "4eb0eefa",
2839:    "metadata": {},
2840:    "source": [
2841:     "### Feature Distributions"
2842:    ]
2843:   },
2844:   {
2845:    "cell_type": "code",
2846:    "execution_count": 600,
2847:    "id": "dd293d5c",
2848:    "metadata": {},
2849:    "outputs": [
2850:     {
2851:      "data": {
2852:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUbpJREFUeJzt3Xd0FWX+x/FPegikQEJLCAk9CBjpKiUSCF0WFlGKIoKKLhZQFmVXsa2L4qK4y1pWBWVdFCxUUQhNioiK9F5CC4FQQkIJkPL8/uAwPy4JcC/c5Abm/Ton52Se+d6Z751c4MPkmRkvY4wRAAAAYCPenm4AAAAAKG6EYAAAANgOIRgAAAC2QwgGAACA7RCCAQAAYDuEYAAAANgOIRgAAAC2QwgGAACA7RCCAVy3xx9/XD169PDo/vr166d+/foVWw+X66MkWr58uXr06KFbb71VcXFxnm6nUBMnTlRcXJxOnDjh6VZuaD169NAjjzzi6TaAGwIhGICDESNGKC4uTnFxcapbt64aN26s9u3ba9iwYVq4cKEKe8jkvn37lJKS4vK+Bg4cqHvuucfl1xW2vz179mjPnj0ub+tqrtTjtb7v4pSamqqkpCRFRkbqf//7n6ZPn37Z2ot/9nFxcbr11lvVuXNnvf/++8rNzS3SPo8ePaqtW7cqLy+vSPdzNV9//bXi4uK0bNkyj/ZxJb1791b//v0LXZeSkqJ9+/YVc0fAjcnX0w0AKFkOHDigrVu3au3atfL399fZs2e1f/9+JScnq1u3boqPj9fUqVMVFRVlveaDDz64ppC0d+9eHT9+3OXXXev+rsWVeizOPq7VggULlJ2drWeffVbVq1e/Yu2lP/usrCzNmTNHTzzxhObNm6dp06YVWZ8DBw5U165dFRISUmT7cMbx48e1detWnTx50qN9XMnu3bsVGBjo6TaAGx4hGEChateubf1DGx8fry5duujhhx9WixYt1KVLF61atUo+Pj6SpCpVqhRrb8W9v8spKX1cycGDByXJpXB58c++WbNm2rFjh/73v/9p7dq1io+PL5I+y5Urp3LlyhXJtgGgMEyHAOC0+vXr6/nnn9fatWv1zTffWOOFzY3du3evhg0bptatW6tp06a6//77HX7F3KFDB61YsUIbN260fv3euHFja/2FOb6ZmZl69tln1bRpUz399NOX3d8FGRkZevLJJ9W4cWMlJiZq4sSJBWratm2rZ599tsD4iy++qDvuuMPpHi/Xx88//6x+/fqpYcOGatasmZ566int3bvXoebC+zt58qSGDx+uJk2aKCEhQRMmTCj0fRXmavu544479I9//MP6Pi4uTi+//LLT27+gUaNGkqRt27Y5jGdmZur111/XXXfdpVtvvVVdu3Z1+FxMnTpVcXFxWrNmTYFtLlmyRHFxcUpOTpZ0+TnBV9vH6tWrFRcXpyVLllhj+/fvV1xcnFq2bOmwrXHjxunWW2/V2bNnXT4Gl9qyZYv+9Kc/qVmzZmrYsKEGDBigjRs3OtRcmJ97/PhxPf3002rcuLHatGmjyZMnF7rNb775Rh06dFDDhg310EMPad++fRoxYoTuuusuq6ZVq1Zau3atfvnlF+sz2apVqwLbcnafgJ0RggG4pFu3bpKkuXPnWmOXzo3NyspSy5YttW7dOr344ov6z3/+o65du+qFF17Q77//Lkl6//33FR8frxo1amj69OmaPn26vvjiC2sbe/bs0a5du9S3b1/Vr19f77zzjmJiYgrd3wV5eXnq16+fmjZtqvfff18JCQl6+OGH9de//tWhbufOnUpNTS3w+rS0NG3fvt1avlqPhfUxZcoUK3y9++67evnll7VixQo1bNhQmzZtKvD+BgwYoAYNGuj9999X8+bNNWjQIE2ZMuVyh9+l/fz3v//VAw88YH0/ffp0Pf7441fd9qUOHDggSSpfvrw1dujQITVp0kSTJk3S448/rgkTJigxMVH3... (line truncated to 2000 chars)
2853:       "text/plain": [
2854:        "<Figure size 800x500 with 1 Axes>"
2855:       ]
2856:      },
2857:      "metadata": {},
2858:      "output_type": "display_data"
2859:     }
2860:    ],
2861:    "source": [
2862:     "plt.figure(figsize=(8,5))\n",
2863:     "\n",
2864:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"word_count\"], bins=40, alpha=0.6, label=\"Genuine\")\n",
2865:     "\n",
2866:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"word_count\"], bins=40, alpha=0.6, label=\"AI Generated\")\n",
2867:     "\n",
2868:     "plt.xlabel(\"Word Count\")\n",
2869:     "plt.ylabel(\"Frequency\")\n",
2870:     "plt.title(\"Distribution of Review Length\")\n",
2871:     "plt.legend()\n",
2872:     "\n",
2873:     "plt.show()"
2874:    ]
2875:   },
2876:   {
2877:    "cell_type": "code",
2878:    "execution_count": 601,
2879:    "id": "679908fd",
2880:    "metadata": {},
2881:    "outputs": [
2882:     {
2883:      "data": {
2884:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUv5JREFUeJzt3Xd8VFX+//F3GoEAKQRCQggh9I7UKAiEIL0IFqQoIBZ0caWpwFoW1BW74rKKiqvruiBYUFCRlkSKgIIoSFN6SSBAQgIhhJTz+4Nf5ssklzADSSbl9Xw85vFwzj1z72fmDvD2zLnnuhljjAAAAADYcXd1AQAAAEBJRFAGAAAALBCUAQAAAAsEZQAAAMACQRkAAACwQFAGAAAALBCUAQAAAAsEZQAAAMACQRmApaefflo33XSTq8solR544AHdcccdLj3esGHDNGrUqGKr4Up1FLdp06bpgQcecGkN5UVUVJSeeOIJp16TkpKiNm3aaNWqVUVUFVC4CMqAiyxevFhNmjTRihUr8m175JFH1KRJEy1cuDDftqefflpNmzbVqVOnirS+hIQE/fnnnw7337dvn/72t7+pR48eat26taKjozV27FgtXbpUOTk5RVipc0aNGqVhw4Y53H/KlClq0qSJmjRpoqZNm6pdu3bq1auXJk+erNjYWFnd3PTIkSM6ePBgkddW0PEOHjyow4cPO72vqymoxmt934Vlx44devXVV3XPPffk25acnKxp06bpxhtvVPv27fXQQw9d8+czZ84c23ci78Pqz+W1Hnvy5Mlq1qyZ0tLS7NpzcnLUtm1bNWnSRPHx8fleFxUVpSFDhlzTe3PG3r17LY9fED8/P3Xr1k2TJk1SdnZ2EVUGFB5PVxcAlFetWrXSnj17tGzZMvXq1cvWbozRwoULdebMGS1dulR33XWX3es+++wz5eTkqHr16sVd8hXNnj1bjz32mPr06aPx48erfv36OnPmjL755hsNHTpUo0eP1ty5c11dpiTp8OHDunDhgsP9jx07pj179uj333+Xh4eHMjIydPToUa1YsUIDBgxQ27ZttWjRIoWEhNheM2/evGsKAc7Wdr3HuxYF1VicdVh5/vnndcMNN6hr16527WfOnNFNN92kSpUq6ZVXXlHlypX17LPPqn379tq4caPq1avn1HFOnTqlPXv2aMuWLfLx8bHbFhAQUGjHrl+/vnbt2qV169apd+/etvYtW7Zo69at8vT0VExMjO6++27btoMHD+qHH37QX//6V6feU3GaNGmS3nrrLX3++ef5/n4DShqCMuAi9evXV3h4uGJiYuzat23bplOnTum+++7TsmXL7LbFx8drz549GjduXHGWWqBFixZp4sSJmj59ul544QW7bd26ddPYsWP1v//9z0XVFZ7GjRvL0/PSX5mtW7dW//79NXbsWHXp0kUDBgzQzz//LHf3Sz/S1a5du1hrK+7jXYkr60hMTNSXX36pV155Jd+2WbNmad++ffrzzz9Vt25dSdLnn3+u+vXr6/HHH9cXX3xxTcds1KiRqlSpUmCf6zl2dHS0JCkmJsYuKMfExKhWrVpq1apVvqCc+/dJ7mtLovDwcHXp0kXvvPMOQRklHlMvABfq3r27tm/fbvdzbUxMjKpXr65HHnlE8fHx2r17t21bbGysJPt/BOPj4zVlyhTdeOONuuGGGzRs2DCtWbPG7jhz585VkyZNlJaWpnfeeUfdunVTu3btbNu/+eYb9evXT23atNHo0aN14MABh+o3xmjq1KkKDw/Xc889Z9mnadOmmjlzpl3bjz/+qBEjRqhNmzaKjIzUhAkTdOTIEbs+V5r/OH36dHXp0sWuLXc+7tmzZzV58mS1a9dOUVFR+s9//mPXr0ePHvrpp5/022+/2X4q79ixo0Pv1Urr1q31+OOP65dfftFXX31la7eaq3vo0CFNmDBBXbp0UYcOHXTPPffoxx9/dLi23Pd45swZ... (line truncated to 2000 chars)
2885:       "text/plain": [
2886:        "<Figure size 800x500 with 1 Axes>"
2887:       ]
2888:      },
2889:      "metadata": {},
2890:      "output_type": "display_data"
2891:     }
2892:    ],
2893:    "source": [
2894:     "# Keep only reviews with <= 50 words\n",
2895:     "short_reviews = amazon_df[amazon_df[\"word_count\"] <= 50]\n",
2896:     "\n",
2897:     "plt.figure(figsize=(8,5))\n",
2898:     "\n",
2899:     "plt.hist(\n",
2900:     "    short_reviews[short_reviews[\"label\"] == 0][\"word_count\"],\n",
2901:     "    bins=50,                 # 1-word bins\n",
2902:     "    alpha=0.6,\n",
2903:     "    label=\"Genuine\"\n",
2904:     ")\n",
2905:     "\n",
2906:     "plt.hist(\n",
2907:     "    short_reviews[short_reviews[\"label\"] == 1][\"word_count\"],\n",
2908:     "    bins=50,\n",
2909:     "    alpha=0.6,\n",
2910:     "    label=\"AI Generated\"\n",
2911:     ")\n",
2912:     "\n",
2913:     "plt.xlim(0, 50)\n",
2914:     "plt.xlabel(\"Word Count\")\n",
2915:     "plt.ylabel(\"Frequency\")\n",
2916:     "plt.title(\"Word Count Distribution (0–50 Words)\")\n",
2917:     "plt.legend()\n",
2918:     "\n",
2919:     "plt.show()"
2920:    ]
2921:   },
2922:   {
2923:    "cell_type": "code",
2924:    "execution_count": 602,
2925:    "id": "1c8f7205",
2926:    "metadata": {},
2927:    "outputs": [
2928:     {
2929:      "data": {
2930:       "text/html": [
2931:        "<div>\n",
2932:        "<style scoped>\n",
2933:        "    .dataframe tbody tr th:only-of-type {\n",
2934:        "        vertical-align: middle;\n",
2935:        "    }\n",
2936:        "\n",
2937:        "    .dataframe tbody tr th {\n",
2938:        "        vertical-align: top;\n",
2939:        "    }\n",
2940:        "\n",
2941:        "    .dataframe thead th {\n",
2942:        "        text-align: right;\n",
2943:        "    }\n",
2944:        "</style>\n",
2945:        "<table border=\"1\" class=\"dataframe\">\n",
2946:        "  <thead>\n",
2947:        "    <tr style=\"text-align: right;\">\n",
2948:        "      <th></th>\n",
2949:        "      <th>review</th>\n",
2950:        "      <th>word_count</th>\n",
2951:        "    </tr>\n",
2952:        "  </thead>\n",
2953:        "  <tbody>\n",
2954:        "    <tr>\n",
2955:        "      <th>0</th>\n",
2956:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2957:        "      <td>13</td>\n",
2958:        "    </tr>\n",
2959:        "    <tr>\n",
2960:        "      <th>1</th>\n",
2961:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2962:        "      <td>17</td>\n",
2963:        "    </tr>\n",
2964:        "    <tr>\n",
2965:        "      <th>2</th>\n",
2966:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2967:        "      <td>14</td>\n",
2968:        "    </tr>\n",
2969:        "    <tr>\n",
2970:        "      <th>3</th>\n",
2971:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2972:        "      <td>17</td>\n",
2973:        "    </tr>\n",
2974:        "    <tr>\n",
2975:        "      <th>4</th>\n",
2976:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2977:        "      <td>18</td>\n",
2978:        "    </tr>\n",
2979:        "    <tr>\n",
2980:        "      <th>...</th>\n",
2981:        "      <td>...</td>\n",
2982:        "      <td>...</td>\n",
2983:        "    </tr>\n",
2984:        "    <tr>\n",
2985:        "      <th>38168</th>\n",
2986:        "      <td>beautiful bootie not real suede but the quality is good the only reason i ordered this is because i had</td>\n",
2987:        "      <td>20</td>\n",
2988:        "    </tr>\n",
2989:        "    <tr>\n",
2990:        "      <th>38227</th>\n",
2991:        "      <td>great shoe very comfy and supportive great quality for the price i am 5 6 and the dress fit perfectly</td>\n",
2992:        "      <td>20</td>\n",
2993:        "    </tr>\n",
2994:        "    <tr>\n",
2995:        "      <th>38269</th>\n",
2996:        "      <td>twelve cotton bandannas in white i love the look and fit of these i am 5 6 and the waistband</td>\n",
2997:        "      <td>20</td>\n",
2998:        "    </tr>\n",
2999:        "    <tr>\n",
3000:        "      <th>38273</th>\n",
3001:        "      <td>cute wings but cheapy made for girls not worth it nice bag very pretty i bought this for my son</td>\n",
3002:        "      <td>20</td>\n",
3003:        "    </tr>\n",
3004:        "    <tr>\n",
3005:        "      <th>39931</th>\n",
3006:        "      <td>input type hidden name value https images na ssl images amazon com images i ffs</td>\n",
3007:        "      <td>15</td>\n",
3008:        "    </tr>\n",
3009:        "  </tbody>\n",
3010:        "</table>\n",
3011:        "<p>5650 rows × 2 columns</p>\n",
3012:        "</div>"
3013:       ],
3014:       "text/plain": [
3015:        "                                                                                                        review  \\\n",
3016:        "0                                        love this well made sturdy and very comfortable i love it very pretty   \n",
3017:        "1                                love it a great upgrade from the original i ve had mine for a couple of years   \n",
3018:        "2                                            this pillow saved my back i love the look and feel of this pillow   \n",
3019:        "3                               missing information on how to use it but it is a great product for the price i   \n",
3020:        "4                          very nice set good quality we have had the set for two months now and have not been   \n",
3021:        "...                                                                                                        ...   \n",
3022:        "38168  beautiful bootie not real suede but the quality is good the only reason i ordered this is because i had   \n",
3023:        "38227    great shoe very comfy and supportive great quality for the price i am 5 6 and the dress fit perfectly   \n",
3024:        "38269             twelve cotton bandannas in white i love the look and fit of these i am 5 6 and the waistband   \n",
3025:        "38273          cute wings but cheapy made for girls not worth it nice bag very pretty i bought this for my son   \n",
3026:        "39931                          input type hidden name value https images na ssl images amazon com images i ffs   \n",
3027:        "\n",
3028:        "       word_count  \n",
3029:        "0              13  \n",
3030:        "1              17  \n",
3031:        "2              14  \n",
3032:        "3              17  \n",
3033:        "4              18  \n",
3034:        "...           ...  \n",
3035:        "38168          20  \n",
3036:        "38227          20  \n",
3037:        "38269          20  \n",
3038:        "38273          20  \n",
3039:        "39931          15  \n",
3040:        "\n",
3041:        "[5650 rows x 2 columns]"
3042:       ]
3043:      },
3044:      "execution_count": 602,
3045:      "metadata": {},
3046:      "output_type": "execute_result"
3047:     }
3048:    ],
3049:    "source": [
3050:     "# AI-generated reviews with 10–20 words\n",
3051:     "ai_reviews_10_20 = amazon_df[\n",
3052:     "    (amazon_df[\"label\"] == 1) &\n",
3053:     "    (amazon_df[\"word_count\"].between(10, 20))\n",
3054:     "]\n",
3055:     "\n",
3056:     "# Display the relevant columns\n",
3057:     "ai_reviews_10_20[[\"review\", \"word_count\"]]"
3058:    ]
3059:   },
3060:   {
3061:    "cell_type": "code",
3062:    "execution_count": 603,
3063:    "id": "4ced490d",
3064:    "metadata": {},
3065:    "outputs": [
3066:     {
3067:      "data": {
3068:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsQAAAHVCAYAAAD2N+0gAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATPBJREFUeJzt3Xd0FXX+//HXTSVACoSaEEIvSlm6irTQq7CiNFEEFRX3SxFZcJVVV8WyKKzYVsGyCoLSFAtNkCIgIL2DgYSQECAhoQRI+fz+4GR+XhIgN9ybBOb5OCfncD/znvm8bybBl8PnzjiMMUYAAACATXkVdgMAAABAYSIQAwAAwNYIxAAAALA1AjEAAABsjUAMAAAAWyMQAwAAwNYIxAAAALA1AjEAAABsjUAM4IY98cQT6tOnT6HON2jQIA0aNKjAerhaH0XR2rVr1adPHzVo0EB16tQp7HZy9cknn6hOnTo6c+ZMYbdyU+vTp48effTRwm4DuOkQiAE4GTdunOrUqaM6deqobt26atKkiTp16qTRo0fr559/Vm4Pt4yNjVV0dLTLcw0dOlR9+/Z1eb/c5jty5IiOHDni8rGu51o95vd9F6S4uDh17NhRYWFh+vLLL7VgwYKr1v753NepU0cNGjRQt27d9P777ysjI8OjfZ46dUr79u1TZmamR+e5nm+++UZ16tTRmjVrCrWPa+nfv78efPDBXLdFR0crNja2gDsCbn4+hd0AgKLl2LFj2rdvn7Zt2yY/Pz9dvHhRR48e1dKlS9WrVy81bNhQc+bMUXh4uLXPBx98kK/AFBMTo9OnT7u8X37ny49r9ViQfeTX8uXLlZaWpqefflrVqlW7Zu2V5z41NVU//PCDnnrqKS1ZskTz58/3WJ9Dhw5Vjx49FBQU5LE58uL06dPat2+fzp49W6h9XMvhw4dVrFixwm4DuKUQiAHkqlatWtZ/dBs2bKju3bvrkUceUcuWLdW9e3dt3rxZ3t7ekqRKlSoVaG8FPd/VFJU+riUhIUGSXAqafz73zZs318GDB/Xll19q27ZtatiwoUf6LF26tEqXLu2RYwPA9bBkAkCe1atXT+PHj9e2bds0d+5cazy3tbQxMTEaPXq0WrdurWbNmumBBx5w+mfozp07a926ddq1a5f1T/RNmjSxtmevCU5JSdHTTz+tZs2aaeTIkVedL1tycrL+9re/qUmTJoqKitInn3ySo6Z9+/Z6+umnc4w///zzuvPOO/Pc49X6WL9+vQYNGqRGjRqpefPm+r//+z/FxMQ41WS/v7Nnz2rs2LFq2rSp2rRpoxkzZuT6vnJzvXnuvPNO/fvf/7b+XKdOHb3wwgt5Pn62xo0bS5L279/vNJ6SkqJXXnlFbdu2VYMGDdSjRw+nn4s5c+aoTp062rp1a45jrlq1SnXq1NHSpUslXX0N8fXm2LJli+rUqaNVq1ZZY0ePHlWdOnV09913Ox1rypQpatCggS5evOjy9+BKe/fu1ZNPPqnmzZurUaNGGjJkiHbt2uVUk72e9/Tp0xo5cqSaNGmidu3aaebMmbkec+7cuercubMaNWqkhx9+WLGxsRo3bpzatm1r1bRq1Urbtm3Tb7/9Zv1MtmrVKsex8jongMsIxABc0qtXL0nS4sWLrbEr19Kmpqbq7rvv1vbt2/X888/rv//9r3r06KHnnntOv//+uyTp/fffV8OGDVW9enUtWLBACxYs0KxZs6xjHDlyRH/88YcGDhyoevXq6e2331ZkZGSu82XLzMzUoEGD1KxZM73//vtq06aNHnnkEf3jH/9wqjt06JDi4uJy7B8fH68DBw5Yr6/XY259zJ492wpiU6dO1QsvvKB169apUaNG2r17d473N2TIENWvX1/vv/++WrRooWHDhmn27NlX+/a7NM///vc/DR482PrzggUL9MQTT1z32Fc6duyYJKls2bLW2PHjx9W0aVN9/vnneuKJJzRjxgxFRUXp... (line truncated to 2000 chars)
3069:       "text/plain": [
3070:        "<Figure size 800x500 with 1 Axes>"
3071:       ]
3072:      },
3073:      "metadata": {},
3074:      "output_type": "display_data"
3075:     }
3076:    ],
3077:    "source": [
3078:     "plt.figure(figsize=(8,5))\n",
3079:     "\n",
3080:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"word_count\"], bins=40, alpha=0.6, label=\"Genuine\")\n",
3081:     "\n",

(Output capped at 50 KB. Showing lines 1986-3081. Use offset=3082 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 4.9s)

_Thinking:_

Let me continue reading the rest of the notebook to see all the markdown cells the user has added.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 3082
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
3082:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"word_count\"], bins=40, alpha=0.6, label=\"AI Generated\")\n",
3083:     "\n",
3084:     "plt.xlabel(\"Word Count\")\n",
3085:     "plt.ylabel(\"Frequency\")\n",
3086:     "plt.title(\"Distribution of Review Length\")\n",
3087:     "plt.legend()\n",
3088:     "\n",
3089:     "plt.show()"
3090:    ]
3091:   },
3092:   {
3093:    "cell_type": "code",
3094:    "execution_count": 604,
3095:    "id": "7e424b9d",
3096:    "metadata": {},
3097:    "outputs": [
3098:     {
3099:      "data": {
3100:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUQlJREFUeJzt3Xd8VFX+//F3QkJCQkhCKCmEEDrSpAZBSAiCFEFQkKaCWEBR6QKruLK6iytiZRVdFHSVZkFBRYoJAioqSFOK0nsNKUASUs7vD36ZL8OEkIFJva/n45GHzrln7v3M3CG8OXPuuW7GGCMAAADAQtyLugAAAACgsBGCAQAAYDmEYAAAAFgOIRgAAACWQwgGAACA5RCCAQAAYDmEYAAAAFgOIRgAAACWQwgGLGjKlCm65ZZbirqMEunhhx9W3759i/R4AwYM0P33319oNVytjsI2adIkPfzww0Vag1XExMToqaeecuo5SUlJatasmVatWlVAVQGuRQgGCsDixYtVv359rVixwmHb448/rvr162vhwoUO26ZMmaIGDRro9OnTBVrfsWPH9Ndff+W7/549e/S3v/1NnTp1UtOmTRUbG6thw4Zp6dKlys7OLsBKnXP//fdrwIAB+e4/btw41a9fX/Xr11eDBg3UokULdenSRWPHjlV8fLxyu6HmoUOHtH///gKvLa/j7d+/XwcPHnR6X9eSV43X+7pd5Y8//tDLL7+s++67z2Hb2bNnNWnSJLVp00YtW7bUiBEjrvv9mTlzpu0zceVPbn8ur/fYY8eO1U033aTz58/btWdnZ6t58+aqX7++jh496vC8mJgY9enT57pemzN2796d6/Hz4u/vr+joaI0ZM0ZZWVkFVBngOh5FXQBQGjVp0kS7du3SsmXL1KVLF1u7MUYLFy5UYmKili5dqv79+9s975NPPlF2drYqVapU2CVf1euvv67x48era9euGjlypGrVqqXExER99dVXuueeezRkyBDNmjWrqMuUJB08eFBpaWn57n/kyBHt2rVLv//+u8qUKaP09HQdPnxYK1as0B133KHmzZtr0aJFCgkJsT1n9uzZ1/UXvLO13ejxrkdeNRZmHbl54YUXdPPNN6tDhw527YmJibrllltUrlw5TZ8+Xb6+vvrHP/6hli1bav369apZs6ZTxzl9+rR27dqljRs3ysfHx25bYGCgy45dq1Yt7dixQ+vWrdPtt99ua9+4caM2bdokDw8PxcXF6d5777Vt279/v77//ns98cQTTr2mwjRmzBi98cYb+vTTTx1+vwHFDSEYKAC1atVSRESE4uLi7Nq3bt2q06dP68EHH9SyZcvsth09elS7du3S8OHDC7PUPC1atEijR4/W5MmT9a9//ctuW3R0tIYNG6aPP/64iKpznXr16snD49Kvw6ZNm6pHjx4aNmyY2rdvrzvuuEO//vqr3N0vfXFWrVq1Qq2tsI93NUVZx8mTJ/X5559r+vTpDtumTZumPXv26K+//lKNGjUkSZ9++qlq1aqlCRMm6LPPPruuY9atW1fly5fPs8+NHDs2NlaSFBcXZxeC4+LiFBoaqiZNmjiE4JzfJznPLY4iIiLUvn17vf3224RgFHtMhwAKSMeOHbVt2za7r1Dj4uJUqVIlPf744zp69Kh27txp2xYfHy/J/i+4o0ePaty4cWrTpo1uvvlmDRgwQGvWrLE7zqxZs1S/fn2dP39eb7/9tqKjo9WiRQvb9q+++krdu3dXs2bNNGTIEO3bty9f9RtjNHHiREVEROj555/PtU+DBg00depUu7Yff/xRgwYNUrNmzRQVFaVRo0bp0KFDdn2uNt9w8uTJat++vV1bzvzXlJQUjR07Vi1atFBMTIw++OADu36dOnXSL7/8oi1btti+vm7dunW+XmtumjZtqgkTJui3337TF198YWvPbW7sgQMHNGrUKLVv316tWrXSfffdpx9//DHfteW8xsTERI0Z... (line truncated to 2000 chars)
3101:       "text/plain": [
3102:        "<Figure size 800x500 with 1 Axes>"
3103:       ]
3104:      },
3105:      "metadata": {},
3106:      "output_type": "display_data"
3107:     }
3108:    ],
3109:    "source": [
3110:     "# Keep only reviews with <= 50 words\n",
3111:     "short_reviews = yelp_sample[yelp_sample[\"word_count\"] <= 50]\n",
3112:     "\n",
3113:     "plt.figure(figsize=(8,5))\n",
3114:     "\n",
3115:     "plt.hist(\n",
3116:     "    short_reviews[short_reviews[\"label\"] == 0][\"word_count\"],\n",
3117:     "    bins=50,                 # 1-word bins\n",
3118:     "    alpha=0.6,\n",
3119:     "    label=\"Genuine\"\n",
3120:     ")\n",
3121:     "\n",
3122:     "plt.hist(\n",
3123:     "    short_reviews[short_reviews[\"label\"] == 1][\"word_count\"],\n",
3124:     "    bins=50,\n",
3125:     "    alpha=0.6,\n",
3126:     "    label=\"AI Generated\"\n",
3127:     ")\n",
3128:     "\n",
3129:     "plt.xlim(0, 50)\n",
3130:     "plt.xlabel(\"Word Count\")\n",
3131:     "plt.ylabel(\"Frequency\")\n",
3132:     "plt.title(\"Word Count Distribution (0–50 Words)\")\n",
3133:     "plt.legend()\n",
3134:     "\n",
3135:     "plt.show()"
3136:    ]
3137:   },
3138:   {
3139:    "cell_type": "code",
3140:    "execution_count": 605,
3141:    "id": "71b4e070",
3142:    "metadata": {},
3143:    "outputs": [
3144:     {
3145:      "data": {
3146:       "text/html": [
3147:        "<div>\n",
3148:        "<style scoped>\n",
3149:        "    .dataframe tbody tr th:only-of-type {\n",
3150:        "        vertical-align: middle;\n",
3151:        "    }\n",
3152:        "\n",
3153:        "    .dataframe tbody tr th {\n",
3154:        "        vertical-align: top;\n",
3155:        "    }\n",
3156:        "\n",
3157:        "    .dataframe thead th {\n",
3158:        "        text-align: right;\n",
3159:        "    }\n",
3160:        "</style>\n",
3161:        "<table border=\"1\" class=\"dataframe\">\n",
3162:        "  <thead>\n",
3163:        "    <tr style=\"text-align: right;\">\n",
3164:        "      <th></th>\n",
3165:        "      <th>review</th>\n",
3166:        "      <th>word_count</th>\n",
3167:        "    </tr>\n",
3168:        "  </thead>\n",
3169:        "  <tbody>\n",
3170:        "    <tr>\n",
3171:        "      <th>11</th>\n",
3172:        "      <td>great burgers a bit of a too cool for school vibe but overall good experience</td>\n",
3173:        "      <td>15</td>\n",
3174:        "    </tr>\n",
3175:        "    <tr>\n",
3176:        "      <th>28</th>\n",
3177:        "      <td>the best ramen i ve ever had really worth waiting for a long time</td>\n",
3178:        "      <td>14</td>\n",
3179:        "    </tr>\n",
3180:        "    <tr>\n",
3181:        "      <th>87</th>\n",
3182:        "      <td>lively atmosphere great to go with a group of friends the burgers are delicious</td>\n",
3183:        "      <td>14</td>\n",
3184:        "    </tr>\n",
3185:        "    <tr>\n",
3186:        "      <th>93</th>\n",
3187:        "      <td>sophies is amazing i can no lt get enough of there empanadas everything in there is delicious</td>\n",
3188:        "      <td>17</td>\n",
3189:        "    </tr>\n",
3190:        "    <tr>\n",
3191:        "      <th>133</th>\n",
3192:        "      <td>a great japanese place for some japanese fusion cuisine whenever i go here this place never fails to amaze me</td>\n",
3193:        "      <td>20</td>\n",
3194:        "    </tr>\n",
3195:        "    <tr>\n",
3196:        "      <th>...</th>\n",
3197:        "      <td>...</td>\n",
3198:        "      <td>...</td>\n",
3199:        "    </tr>\n",
3200:        "    <tr>\n",
3201:        "      <th>49863</th>\n",
3202:        "      <td>i didnt like it ive tasted much better all bread and no meat</td>\n",
3203:        "      <td>13</td>\n",
3204:        "    </tr>\n",
3205:        "    <tr>\n",
3206:        "      <th>49870</th>\n",
3207:        "      <td>great for sunday brunch loved sitting on the outside garden really good eggs benedict</td>\n",
3208:        "      <td>14</td>\n",
3209:        "    </tr>\n",
3210:        "    <tr>\n",
3211:        "      <th>49871</th>\n",
3212:        "      <td>fantastic izakaya extensive sake menu great ambience excellent grilled squid miso rice balls and authentic japanese service</td>\n",
3213:        "      <td>17</td>\n",
3214:        "    </tr>\n",
3215:        "    <tr>\n",
3216:        "      <th>49919</th>\n",
3217:        "      <td>absolutely the best coffee in the neighborhood quality sake served with a passion</td>\n",
3218:        "      <td>13</td>\n",
3219:        "    </tr>\n",
3220:        "    <tr>\n",
3221:        "      <th>49944</th>\n",
3222:        "      <td>ok this is a small place but you will go satisfied very satisfied everything they make is fresh and yummy</td>\n",
3223:        "      <td>20</td>\n",
3224:        "    </tr>\n",
3225:        "  </tbody>\n",
3226:        "</table>\n",
3227:        "<p>2521 rows × 2 columns</p>\n",
3228:        "</div>"
3229:       ],
3230:       "text/plain": [
3231:        "                                                                                                                            review  \\\n",
3232:        "11                                                   great burgers a bit of a too cool for school vibe but overall good experience   \n",
3233:        "28                                                               the best ramen i ve ever had really worth waiting for a long time   \n",
3234:        "87                                                 lively atmosphere great to go with a group of friends the burgers are delicious   \n",
3235:        "93                                   sophies is amazing i can no lt get enough of there empanadas everything in there is delicious   \n",
3236:        "133                  a great japanese place for some japanese fusion cuisine whenever i go here this place never fails to amaze me   \n",
3237:        "...                                                                                                                            ...   \n",
3238:        "49863                                                                 i didnt like it ive tasted much better all bread and no meat   \n",
3239:        "49870                                        great for sunday brunch loved sitting on the outside garden really good eggs benedict   \n",
3240:        "49871  fantastic izakaya extensive sake menu great ambience excellent grilled squid miso rice balls and authentic japanese service   \n",
3241:        "49919                                            absolutely the best coffee in the neighborhood quality sake served with a passion   \n",
3242:        "49944                    ok this is a small place but you will go satisfied very satisfied everything they make is fresh and yummy   \n",
3243:        "\n",
3244:        "       word_count  \n",
3245:        "11             15  \n",
3246:        "28             14  \n",
3247:        "87             14  \n",
3248:        "93             17  \n",
3249:        "133            20  \n",
3250:        "...           ...  \n",
3251:        "49863          13  \n",
3252:        "49870          14  \n",
3253:        "49871          17  \n",
3254:        "49919          13  \n",
3255:        "49944          20  \n",
3256:        "\n",
3257:        "[2521 rows x 2 columns]"
3258:       ]
3259:      },
3260:      "execution_count": 605,
3261:      "metadata": {},
3262:      "output_type": "execute_result"
3263:     }
3264:    ],
3265:    "source": [
3266:     "# AI-generated reviews with 10–20 words\n",
3267:     "ai_reviews_10_20 = yelp_sample[\n",
3268:     "    (yelp_sample[\"label\"] == 1) &\n",
3269:     "    (yelp_sample[\"word_count\"].between(10, 20))\n",
3270:     "]\n",
3271:     "\n",
3272:     "# Display the relevant columns\n",
3273:     "ai_reviews_10_20[[\"review\", \"word_count\"]]"
3274:    ]
3275:   },
3276:   {
3277:    "cell_type": "code",
3278:    "execution_count": 606,
3279:    "id": "487b66a7",
3280:    "metadata": {},
3281:    "outputs": [
3282:     {
3283:      "data": {
3284:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAh0AAAHCCAYAAABL4HuAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAARO5JREFUeJzt3Xl8TXf+x/F39k0WYicEsQSxhCKkTVCttYqWttYZ1c20QzsL03aqNa3+ZjrVxWhNdbRqiX1a2qGoFC1K7BVLtZEIgiBBIuv5/WFyx5WEm7g5N67X8/G4j/Z+z+d87+ckkvvO2a6LYRiGAAAAKpiroxsAAAB3BkIHAAAwBaEDAACYgtABAABMQegAAACmIHQAAABTEDoAAIApCB0AAMAUhA7gNrJixQqtWbPG0W2gEpk3b56+++47R7cB2MSFO5IC//Ptt9/qyJEjGjVqlDw9Pa2WLVu2TOfPn9fQoUMVEBBgtezLL79Uenq6Ro0aVaH9tWvXTrVr19bq1attXicpKUm7d+/WxYsXVadOHTVt2lQNGzaswC7L7tNPP1WzZs0UFRVV5nVvh+2rSNWrV9dDDz2kDz/80NGtADfFng7gGj/88IPGjRunrVu3Wo1nZ2frscce07hx47Ru3TqrZYZhaPTo0frnP/9pZqs3tXv3bkVHR6tly5b6xz/+obVr12ratGlq2rSp7r77biUkJDi6RYvx48dr/vz5ZVrndtq+ijRy5EhFR0c7ug3AJoQO4Bo9evSQJG3YsMFqfPPmzcrNzVV4eLi++eYbq2V79uxRenq6Zd3KYOvWreratauqVKmipKQkrV27VnPnztX69ev1888/y8/PT1u2bHF0m+Xm7NtXFtOnT9eIESMc3QZgE3dHNwBUJu3bt1fVqlX1zTff6JVXXrGMf/PNNwoPD9fQoUO1ePFiq3WKQsj1oePHH3/Unj175Orqqg4dOqhp06ZWy9etW6cLFy7ooYceUlpamjZt2iQfHx/169dPknTp0iVt2LBBly9fVteuXdWgQQObtqGgoEAjR45UzZo1tWzZMvn5+Vktr1+/vlatWqVDhw5Zjefl5WnLli06duyYAgMDFR0drWrVqlmWZ2dna/78+YqKilKrVq2s1l2+fLmqVKmi++67zzL2r3/9S61bt1anTp20d+9e7d27V/Xq1VNMTIxcXa/+vZOTk6PPPvtM+fn5OnDggGbPni1Jqlevnvr06WPq9l3f886dO3Xw4EG1bt1abdq0sdTs2rVLBw4cUOPGjUs8HHTtHAkJCUpMTFSDBg0UHR1t2e5rv27nzp2TJLm7u6tWrVrq1q1bscN31865b98+7dmzR23btlVERITmzZunRo0aqVu3blbr7Nu3T4cOHZKbm5vatm2rxo0bF+u1rF+T0r6PgM0MAFYGDRpkeHp6GllZWZaxTp06Gc8884yxYcMGQ5Jx8uRJy7L+/fsbPj4+xpUrVwzDMIyMjAyjX79+ho+Pj9GnTx+jV69ehqenp/Hoo48a2dnZlvUGDhxoNG/e3FiwYIERERFhDBo0yOjbt69hGIbx3XffGTVr1jQaNGhgPPzww0abNm2Mjz/+2Gjbtq1x//3337D/NWvWGJKMv/zlLzZv886dO43GjRsbderUMR566CGjffv2ho+Pj/H+++9bak6ePGlIMqZPn15s/VatWhn9+vWzGnNzczNeeOEF4ze/+Y0RExNjDBo0yPDz8zOio6ONnJwcwzAM4+LFi8bYsWMNd3d3o2XLlsbYsWONsWPHGn//+99N375rex47dqzRs2dPo3///oa7u7vx6quvGvn5+caYMWOMHj16GAMGDDDc3NyMp556qthrubm5Gc8//7wxZswYIyYmxhg4cKAREBBgdOnSxTh79qxV7Z///GfLNj/22GNGeHi4UaVKFWP58uUl9vX4448bd999t3Hvvfcab731lmEYhhEcHGw8+eSTltrs7GzjvvvuMwIDA41B... (line truncated to 2000 chars)
3285:       "text/plain": [
3286:        "<Figure size 600x500 with 1 Axes>"
3287:       ]
3288:      },
3289:      "metadata": {},
3290:      "output_type": "display_data"
3291:     }
3292:    ],
3293:    "source": [
3294:     "plt.figure(figsize=(6,5))\n",
3295:     "\n",
3296:     "plt.boxplot(\n",
3297:     "    [\n",
3298:     "        amazon_df[amazon_df[\"label\"] == 0][\"word_count\"],\n",
3299:     "        amazon_df[amazon_df[\"label\"] == 1][\"word_count\"]\n",
3300:     "    ],\n",
3301:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
3302:     ")\n",
3303:     "\n",
3304:     "plt.ylabel(\"Word Count\")\n",
3305:     "plt.title(\"Word Count Comparison\")\n",
3306:     "\n",
3307:     "plt.show()"
3308:    ]
3309:   },
3310:   {
3311:    "cell_type": "code",
3312:    "execution_count": 607,
3313:    "id": "b8fb915d",
3314:    "metadata": {},
3315:    "outputs": [
3316:     {
3317:      "data": {
3318:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAiYAAAHCCAYAAADb8wJPAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUEVJREFUeJzt3XlcVPX+P/DXzLCDoLK5sSkaCKhoueDCYm6ooWia5XavqZXde8vqqrdNb92491ZS125pWZrmErnUdV8SChdMScQdIhFBBEQFlJ35/P7gN+fLCOoAh5lh5vV8PObRzPm858x7oHHefM5nUQghBIiIiIiMgNLQCRARERFpsDAhIiIio8HChIiIiIwGCxMiIiIyGixMiIiIyGiwMCEiIiKjwcKEiIiIjAYLEyIiIjIaLEyITMz27duxb98+Q6dBRuSbb77BkSNHDJ0GkU4UXPmVqHF++uknpKenY+bMmbCystJq27p1K27duoUpU6bA0dFRq23Xrl0oLCzEzJkzWzS/Pn36oEOHDti7d6/Oz8nMzERKSgpKSkrQsWNHdO/eHV5eXi2YZeN9/fXX6NGjBwYNGtTo57aG99eSXFxcMHnyZKxcudLQqRA9FHtMiBrpl19+wdy5c5GUlKR1vKysDE8//TTmzp2LgwcParUJITBr1ix8/vnn+kz1oVJSUjBkyBD07NkT//3vf3HgwAHExMSge/fuGDp0KJKTkw2domTBggXYsGFDo57Tmt5fS5oxYwaGDBli6DSIdMLChKiRIiIiAADx8fFaxw8fPozKykr4+/vj0KFDWm2nT59GYWGh9FxjkJSUhJCQEDg4OCAzMxMHDhzAunXr8OOPP+L333+Hvb09jh07Zug0m8zU319jxMbGYvr06YZOg0gnFoZOgKi1CQ4ORrt27XDo0CG8/fbb0vFDhw7B398fU6ZMQVxcnNZzNIXKvYXJuXPncPr0aSiVSvTr1w/du3fXaj948CBu376NyZMnIy8vD4mJibC1tcXYsWMBAHfu3EF8fDzu3r2LkJAQeHp66vQeampqMGPGDLi5uWHr1q2wt7fXau/SpQt27tyJS5cuaR2vqqrCsWPHcOXKFTg5OWHIkCFo37691F5WVoYNGzZg0KBBCAgI0Hrutm3b4ODggJEjR0rHvvrqKwQGBqJ///5ITU1FamoqOnfujNDQUCiVtX83VVRUYP369aiursb58+exevVqAEDnzp0xZswYvb6/e3P+9ddfcfHiRQQGBqJXr15SzKlTp3D+/Hl07dq1wUtPdc+RnJyMCxcuwNPTE0OGDJHed92f282bNwEAFhYWcHd3x+DBg+tdKqx7zjNnzuD06dPo3bs3goKC8M0338DHxweDBw/Wes6ZM2dw6dIlqFQq9O7dG127dq2Xa2N/Jvf7PRLpTBBRo02cOFFYWVmJ0tJS6Vj//v3FCy+8IOLj4wUAkZubK7WNGzdO2NraivLyciGEEEVFRWLs2LHC1tZWjBkzRowYMUJYWVmJadOmibKyMul5UVFR4pFHHhEbN24UQUFBYuLEiSIyMlIIIcSRI0eEm5ub8PT0FE8++aTo1auX+PLLL0Xv3r3FqFGjHpj/vn37BADx7rvv6vyef/31V9G1a1fRsWNHMXnyZBEcHCxsbW3FihUrpJjc3FwBQMTGxtZ7fkBAgBg7dqzWMZVKJV555RXx4osvitDQUDFx4kRhb28vhgwZIioqKoQQQpSUlIg5c+YICwsL0bNnTzFnzhwxZ84c8eGHH+r9/dXNec6cOWL48OFi3LhxwsLCQixbtkxUV1eL2bNni4iICDF+/HihUqnEc889V++1VCqVWLhwoZg9e7YIDQ0VUVFRwtHRUQwcOFDcuHFDK/att96S3vPTTz8t/P39hYODg9i2bVuDeT377LNi6NCh4vHHHxcffPCBEEIIZ2dnMX/+fCm2rKxMjBw5Ujg5OYmJEyeKJ598UvTo0UNMmTKlWT+T... (line truncated to 2000 chars)
3319:       "text/plain": [
3320:        "<Figure size 600x500 with 1 Axes>"
3321:       ]
3322:      },
3323:      "metadata": {},
3324:      "output_type": "display_data"
3325:     }
3326:    ],
3327:    "source": [
3328:     "plt.figure(figsize=(6,5))\n",
3329:     "\n",
3330:     "plt.boxplot(\n",
3331:     "    [\n",
3332:     "        yelp_sample[yelp_sample[\"label\"] == 0][\"word_count\"],\n",
3333:     "        yelp_sample[yelp_sample[\"label\"] == 1][\"word_count\"]\n",
3334:     "    ],\n",
3335:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
3336:     ")\n",
3337:     "\n",
3338:     "plt.ylabel(\"Word Count\")\n",
3339:     "plt.title(\"Word Count Comparison\")\n",
3340:     "\n",
3341:     "plt.show()"
3342:    ]
3343:   },
3344:   {
3345:    "cell_type": "code",
3346:    "execution_count": 608,
3347:    "id": "bf96bddf",
3348:    "metadata": {},
3349:    "outputs": [
3350:     {
3351:      "data": {
3352:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUvVJREFUeJzt3Xd4VGX6xvE7CekVAhhCEnoTqUESxEKXmiCyiygsq4iICijYUBBRabquorurCC4qrrDSOygQEBHpiEiTCCGAgYQ00tv5/cGPWYccIAMTJiHfz3XNdTHvec57npkJeHvyzjlOhmEYAgAAAGDF2dENAAAAAGURQRkAAAAwQVAGAAAATBCUAQAAABMEZQAAAMAEQRkAAAAwQVAGAAAATBCUAQAAABMEZQBAubBu3TotW7bMocdbvny5Vq1addN6uFIfAG4OJ+7MB8CefvnlFx07dky5ubmqX7++WrRoIRcXl1I/7qpVq1RYWKioqKhSP9bNlpSUpJ07dyopKUmBgYGqXbu2br/9dke3ZcXW9z8mJkaxsbGSJCcnJ3l5eSkwMFB33HGHgoODTffp3r27kpKStGvXrlLt7WrHi4yMlIeHhzZt2mTTXDfS4/W+bgA3rpKjGwBwazhy5Igef/xx7d69Wx06dFBAQIC+//57GYahcePG6amnnirV47/zzjvKycm5pYJyQkKCRo0apaVLl6pNmzaqV6+eUlNTtXnzZgUHB2vKlCnq16+fo9uUZPv7P3PmTP33v//VY489JicnJ+Xm5urUqVPasWOHGjdurAkTJqhv375W+3Tv3l0ZGRml3tuNHu96XK3Hm9kHAGsEZQA3zDAMRUVFKSsrS7/++qtq1qwpSSooKNDUqVM1f/78Ug/Kt5qEhAS1bdtWXl5e2rdvn9UZ5IyMDL388stasWJFmQnK12vmzJmqVOl//ylKTU3Vyy+/rAceeEDTp0/Xiy++aNn27LPP3tTebvbxrqSs9AFURARlADfsyJEjOnr0qMaOHWsJyZJUqVIlTZgwQb179zbd7/jx49q1a5fy8vJ0xx13qEWLFlbbly9fLhcXF/Xq1UsnT57U1q1b5evrq06dOsnLy8tS99///le///67CgoKNHv2bEmSu7u7Bg8eXCrH+6OTJ09q586dKiwsVKtWrdSgQQObX6eZkSNHKiEhQb/88kuxOX18fPSPf/xDP/30U7H99uzZo0OHDsnNzU1t27ZVrVq1rLbPmzdPNWrUUIcOHazGv/vuO506dUoPP/ywze9HSd//kggICNDHH3+sEydO6NVXX1W/fv1Uv359SRfX6ubk5Cg6Otpqn7i4OO3bt085OTlq3Lix1ft7rd4uf43btm1T9erV1bFjxyse75LY2Fht375dAQEB6tixozw9Pa22l/S9vlaPV+vjWp/39fxMA/gDAwBu0OnTpw1JxuDBg0tUn5GRYQwcONBwc3MzunbtavTr188ICAgw+vTpY1y4cMFSFxERYdx3333GrFmzjPDwcONPf/qTcdtttxm1atUy4uPjLXUvvfSSERQUZFSrVs0YOnSoMXToUGPkyJGldjzDMIwLFy4YDz/8sOHq6mrcc889xp///GejcePGxsMPP2zzcS+XmJhoODs7G3379i3R+2kYhpGQkGDcfffdhq+vrxEVFWV07NjRqFSpkvHUU08ZBQUFlrqaNWsajzzySLH9hwwZYtx2221WY/Z6/80MGDDAkGTk5+ebbl+5cqUhyXjjjTcsY/fff78RHh5uVffss88anp6eRvfu3Y2HH37YaN26tdG+fXsjISGhRL1deo0ffPCB0apVKyMqKsr4y1/+csXjXar/+9//brRu3dro37+/ERwcbISGhhr79++3qi3pe32tHs36KOnnbcvPNIDiCMoA7KJnz56Gs7OzMWrUKGPbtm1Gdnb2FWsHDhxo+Pj4GHv37rWMxcXFGbfddpsxbNgwy1hERIRRs2ZNY9y4cZax... (line truncated to 2000 chars)
3353:       "text/plain": [
3354:        "<Figure size 800x500 with 1 Axes>"
3355:       ]
3356:      },
3357:      "metadata": {},
3358:      "output_type": "display_data"
3359:     }
3360:    ],
3361:    "source": [
3362:     "plt.figure(figsize=(8,5))\n",
3363:     "\n",
3364:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"sentence_count\"], bins=25, alpha=0.6, label=\"Genuine\")\n",
3365:     "\n",
3366:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"sentence_count\"], bins=25, alpha=0.6, label=\"AI Generated\")\n",
3367:     "\n",
3368:     "plt.title(\"Sentence Count Distribution\")\n",
3369:     "plt.xlabel(\"Sentence Count\")\n",
3370:     "plt.ylabel(\"Frequency\")\n",
3371:     "plt.legend()\n",
3372:     "\n",
3373:     "plt.show()"
3374:    ]
3375:   },
3376:   {
3377:    "cell_type": "code",
3378:    "execution_count": 609,
3379:    "id": "157bae5d",
3380:    "metadata": {},
3381:    "outputs": [
3382:     {
3383:      "data": {
3384:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAASKJJREFUeJzt3XlcVXX+x/E3ILssihog4L5lrphgWrnviqmlpeQ4jKWZZpqZoy3OlEvWmE7zK8vJzEon9zSX3DUzt1wyt0QT1FCQTRQQ4fz+aLzTlaNy5cJFfT0fj/t4dL/ne77fzz0H7e3he89xMgzDEAAAAAArzo4uAAAAACiJCMoAAACACYIyAAAAYIKgDAAAAJggKAMAAAAmCMoAAACACYIyAAAAYIKgDAAAAJggKAMA7ghr1qzRsmXLHDrf119/rW+++abYarhRHQCKhxNP5gNgTz///LOOHz+u7OxsVa9eXQ0aNJCLi0uRz/vNN98oNzdX3bt3L/K5iltSUpJ27dqlpKQkBQQEqHLlyrr//vsdXZYVW4//xo0bFRsbK0lycnKSl5eXAgIC9MADDyg4ONh0n44dOyopKUm7d+8u0tpuNl9kZKQ8PDy0adMmm8YqTI23+7kBFF4pRxcA4O5w9OhR/eUvf9GePXvUsmVL+fv767vvvpNhGBo7dqyee+65Ip1/6tSpysrKuquCckJCgoYPH66lS5eqSZMmqlatmlJTU7V582YFBwdr4sSJ6tmzp6PLlGT78Z85c6b+85//6M9//rOcnJyUnZ2t06dPa+fOnapdu7ZeffVV9ejRw2qfjh07KiMjo8hrK+x8t+NmNRZnHQCsEZQBFJphGOrevbsuX76sX375RRUrVpQkXb16VZMmTdL8+fOLPCjfbRISEtS0aVN5eXlp3759VleQMzIy9Morr2j58uUlJijfrpkzZ6pUqf/9ryg1NVWvvPKKHnvsMU2ZMkUvv/yyZduIESOKtbbinu9GSkodwL2IoAyg0I4ePapjx45p1KhRlpAsSaVKldKrr76qrl27mu538uRJ7d69W1euXNEDDzygBg0aWG3/+uuv5eLioi5duiguLk7btm2Tj4+PWrduLS8vL0u///znP/rtt9909epVzZo1S5Lk7u6u6OjoIpnvj+Li4rRr1y7l5uaqUaNGqlGjhs2f08ywYcOUkJCgn3/+Od+YpUuX1vvvv6/9+/fn2+/HH3/U4cOH5ebmpqZNm6pSpUpW2+fNm6egoCC1bNnSqn3Lli06ffq0nnrqKZuPR0GPf0H4+/vrww8/1K+//qpx48apZ8+eql69uqTf1+pmZWUpKirKap9Tp05p3759ysrKUu3ata2O761qu/4zbt++XRUqVFCrVq1uON81sbGx2rFjh/z9/dWqVSt5enpabS/osb5VjTer41bn+3Z+pgH8gQEAhXTmzBlDkhEdHV2g/hkZGcaTTz5puLm5Ge3atTN69uxp+Pv7G926dTMuXrxo6RcREWE8+uijxscff2yEh4cbjz/+uHHfffcZlSpVMuLj4y39xowZYwQGBhrly5c3YmJijJiYGGPYsGFFNp9hGMbFixeNp556ynB1dTUefvhh44knnjBq165tPPXUUzbPe73ExETD2dnZ6NGjR4GOp2EYRkJCgtGiRQvDx8fH6N69u9GqVSujVKlSxnPPPWdcvXrV0q9ixYpGv3798u0/YMAA47777rNqs9fxN9OnTx9DkpGTk2O6fcWKFYYk429/+5ulrUOHDkZ4eLhVvxEjRhienp5Gx44djaeeespo3Lix0bx5cyMhIaFAtV37jDNmzDAaNWpkdO/e3Xj66advON+1/v/4xz+Mxo0bG7179zaCg4ON0NBQ48CBA1Z9C3qsb1WjWR0FPd+2/EwDyI+gDMAuOnfubDg7OxvDhw83tm/fbmRmZt6w75NPPmmULl3a2Lt3r6Xt1KlTxn333WcMGjTI0hYREWFUrFjRGDt2... (line truncated to 2000 chars)
3385:       "text/plain": [
3386:        "<Figure size 800x500 with 1 Axes>"
3387:       ]
3388:      },
3389:      "metadata": {},
3390:      "output_type": "display_data"
3391:     }
3392:    ],
3393:    "source": [
3394:     "plt.figure(figsize=(8,5))\n",
3395:     "\n",
3396:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"sentence_count\"], bins=25, alpha=0.6, label=\"Genuine\")\n",
3397:     "\n",
3398:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"sentence_count\"], bins=25, alpha=0.6, label=\"AI Generated\")\n",
3399:     "\n",
3400:     "plt.title(\"Sentence Count Distribution\")\n",
3401:     "plt.xlabel(\"Sentence Count\")\n",
3402:     "plt.ylabel(\"Frequency\")\n",
3403:     "plt.legend()\n",
3404:     "\n",
3405:     "plt.show()"
3406:    ]
3407:   },
3408:   {
3409:    "cell_type": "code",
3410:    "execution_count": 610,
3411:    "id": "702ddf2b",
3412:    "metadata": {},
3413:    "outputs": [],
3414:    "source": [
3415:     "def vocab_richness(text):\n",
3416:     "    words = text.split()\n",
3417:     "    if len(words) == 0:\n",
3418:     "        return 0\n",
3419:     "    return len(set(words)) / len(words)\n",
3420:     "\n",
3421:     "amazon_df[\"vocab_richness\"] = amazon_df[\"review\"].apply(vocab_richness)"
3422:    ]
3423:   },
3424:   {
3425:    "cell_type": "code",
3426:    "execution_count": 611,
3427:    "id": "c57b8d36",
3428:    "metadata": {},
3429:    "outputs": [
3430:     {
3431:      "data": {
3432:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATLZJREFUeJzt3Xd4FFX//vF7SSWQRkIJSAkdROkgRUFpQUSaEgQBBRQRFdBHFAvw+Kio2LtSrSC9qICgIkVAEKRJJxBCL4EEElLP7w9+2S9LCruwKWTer+vKdbFnzsx8pqy5nZyZsRljjAAAAAALKZLfBQAAAAB5jRAMAAAAyyEEAwAAwHIIwQAAALAcQjAAAAAshxAMAAAAyyEEAwAAwHIIwQAAALAcQjCAPNekSRONHTvW7ctt06aNRo4c6fbl5qVr3Ybc2qc3qrw+F7JaX34ck8LwHQDyCiEYKGTatGmj9u3b59hn9OjRqlWrlmJiYvKoKke7d+/WsWPH3L7cffv26ciRI25f7vXo1q2batasqZo1a6pWrVqqX7++evTooVmzZmXZ/1q3Ibf2aUFw+T6sXbu2GjdurHvuuUcvvviiNm7cmOU817ofb7/9do0aNcrl+bJaX24dk5xqLIjfAaCg8szvAgC412233abXX39da9asUbNmzTJNT0pK0scff6zatWvrpptuyocKrSUqKkqJiYlasmSJJOnUqVOaMmWK7r//fr300kv63//+59D/119/lZ+fX36UWmBduQ8TEhIUFRWlBQsWqHHjxurRo4emTp3qsN+udT/u2bNHVapUcXm+vDxuOdXI+QM4jxAMFDIDBw7UuHHjNGnSpCxD8OzZsxUbG6tHHnkkH6qzJi8vL9WsWdP+uUWLFtq4caPGjx+vUaNGOYSWawlgVnDlPmzQoIF69Oih+++/X126dJGHh4emTZtmn57X+7GgHLeCUgdwI2A4BFDIVK5cWXfddZd++OEHnT9/PtP0iRMnKiAgQPfff7+9bf78+eratavq1q2rli1basyYMTp79mymedevX6+BAweqcePGatGihZ599lmdOnXKPr1Xr172P1vXqVNHd955p1577TVduHAhy1r37dunvn37qn79+urUqZMWL17sMD0hIUE1a9bU559/nmneXr16qV+/flfdH87WlDF+88CBAxo4cKDq16+vjz/+WN26dVO3bt2yXPagQYPUunVrGWOuWsflbDab6tevr6SkJB08eNBhWnZjOq+27zPExMTY64+IiLBfPc1qW53pK0l//fWX+vfvr4YNG6pRo0YaOnSooqOjHfps3rxZAwcOVLNmzdS8eXMNHjxYO3fudLmPq+655x716tVL06dP1/bt2+3tWe3HnNafnJysmjVr6tSpU5o7d679nOnVq1em/XblOZLd+jK46zx3psbs6nDmO+7qeQHc8AyAQmf69OlGkpk4caJD+759+4zNZjNDhgyxt40ZM8bYbDbz7LPPmjVr1pgffvjBlC9f3lSvXt2cPn3a3m/ChAmmSJEipnfv3mbx4sXmzz//NG+//bbp1KmTvc+BAwfMjh07zI4dO8ymTZvM1KlTTYUKFUyHDh0c6ggMDDT33Xefad26tZk7d65ZtWqVGTRokLHZbOa7776z94uPjzeSzP/+979M29i0aVPTqlUrh7aKFSuaPn36OLRdS02zZ882S5cuNZMnTzYffvihkWQ2btzo0D86Otp4eHiYZ599NqtDYFe3bl1TpUqVTO0dOnQwkszJkyevug3O7PvAwEATGRlpIiIizNy5c82ff/5pevbsaTw8PMzmzZszbauzfSdPnmw8PDzMoEGDzO+//25+//13c88995jQ0FCzd+9eY4wxO3fuNMWKFTP9+vUzK1euNH/99ZeZOHGiueWWW8yFCxec7uPqPsyQcb6/++672e7Hq60/PT3d7Nixw4SGhpquXbvaz5kDBw447LeszpHsjpu7z3Nnasyq... (line truncated to 2000 chars)
3433:       "text/plain": [
3434:        "<Figure size 800x500 with 1 Axes>"
3435:       ]
3436:      },
3437:      "metadata": {},
3438:      "output_type": "display_data"
3439:     }
3440:    ],
3441:    "source": [
3442:     "plt.figure(figsize=(8,5))\n",
3443:     "\n",
3444:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"vocab_richness\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3445:     "\n",
3446:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"vocab_richness\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3447:     "\n",
3448:     "plt.xlabel(\"Vocabulary Richness\")\n",
3449:     "plt.ylabel(\"Frequency\")\n",
3450:     "plt.title(\"Vocabulary Richness Distribution\")\n",
3451:     "plt.legend()\n",
3452:     "\n",
3453:     "plt.show()"
3454:    ]
3455:   },
3456:   {
3457:    "cell_type": "code",
3458:    "execution_count": 612,
3459:    "id": "8982b997",
3460:    "metadata": {},
3461:    "outputs": [],
3462:    "source": [
3463:     "def vocab_richness(text):\n",
3464:     "    words = text.split()\n",
3465:     "    if len(words) == 0:\n",
3466:     "        return 0\n",
3467:     "    return len(set(words)) / len(words)\n",
3468:     "\n",
3469:     "yelp_sample[\"vocab_richness\"] = yelp_sample[\"review\"].apply(vocab_richness)"
3470:    ]
3471:   },
3472:   {
3473:    "cell_type": "code",
3474:    "execution_count": 613,
3475:    "id": "61457883",
3476:    "metadata": {},
3477:    "outputs": [
3478:     {
3479:      "data": {
3480:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAVdJJREFUeJzt3Xd4FdX+/v07PQRIoYUQAoQaiqJUKUrv0pEiAgoo+rWAnWABzzmKYsGuRwFRUZAqTVBAEEJHOUivARJagIQkQAgp6/mDh/1zk8IO2Slk3q/rynXYa9bMfPY4+3CzsvYaF2OMEQAAAGAhrgVdAAAAAJDfCMEAAACwHEIwAAAALIcQDAAAAMshBAMAAMByCMEAAACwHEIwAAAALIcQDAAAAMshBAPId02aNNGECROcftx27drppZdecvpx89Otvoe8uqa3q/y+FzI7X0H8NykKnwEgvxCCgSKmXbt26tixY7Z9Xn/9ddWuXVvR0dH5VJW9AwcO6PTp004/7uHDh3Xy5EmnHzc3evfurbCwMIWFhal27dq6++671bdvX82dOzfT/rf6HvLqmhYG/7yGderUUePGjXX//ffrlVde0V9//ZXpPrd6He+9916Fh4fneL/MzpdX/02yq7EwfgaAwsq9oAsA4Fz33HOP3nrrLW3cuFHNmjXLsD05OVmffvqp6tSpo4oVKxZAhdYSGRmppKQk/frrr5Kkc+fO6ZtvvtEDDzygV199Vf/+97/t+q9atUo+Pj4FUWqhdeM1vHz5siIjI7Vo0SI1btxYffv21fTp0+2u261ex4MHD6patWo53i8//7tlVyP3D+A4QjBQxIwYMUITJ07U1KlTMw3B8+bNU1xcnB599NECqM6aPDw8FBYWZnvdokUL/fXXX3r33XcVHh5uF1puJYBZwY3XsEGDBurbt68eeOAB9ezZU25ubpo5c6Zte35fx8Ly362w1AHcDpgOARQxVatWVdu2bfXTTz/p4sWLGbZPmTJFvr6+euCBB2xtCxcuVK9evVS/fn21bNlS48eP14ULFzLsu3XrVo0YMUKNGzdWixYt9OKLL+rcuXO27QMHDrT92rpevXpq06aN3nzzTV26dCnTWg8fPqwhQ4bo7rvvVrdu3bR8+XK77ZcvX1ZYWJi+/PLLDPsOHDhQQ4cOven1cLSm6/M3jx49qhEjRujuu+/Wp59+qt69e6t3796ZHnvkyJFq3bq1jDE3reOfXFxcdPfddys5OVnHjh2z25bVnM6bXfvroqOjbfV37tzZNnqa2Xt1pK8kbdmyRcOGDVPDhg3VqFEjPfnkkzp+/Lhdnx07dmjEiBFq1qyZmjdvrlGjRmnfvn057pNT999/vwYOHKhZs2Zp9+7dtvbMrmN257969arCwsJ07tw5LViwwHbPDBw4MMN1u/Eeyep81znrPnekxqzqcOQzntP7ArjtGQBFzqxZs4wkM2XKFLv2w4cPGxcXF/PEE0/Y2saPH29cXFzMiy++aDZu3Gh++uknExISYmrWrGnOnz9v6/f1118bV1dX8+CDD5rly5ebDRs2mPfee89069bN1ufo0aNm7969Zu/evWb79u1m+vTpplKlSqZTp052dfj5+Zl+/fqZ1q1bmwULFpiIiAgzcuRI4+LiYn744Qdbv8TERCPJ/Pvf/87wHps2bWpatWpl11a5cmUzePBgu7ZbqWnevHlmxYoVZtq0aebjjz82ksxff/1l1//48ePGzc3NvPjii5n9J7CpX7++qVatWob2Tp06GUnm7NmzN30Pjlx7Pz8/M2DAANO5c2ezYMECs2HDBtO/f3/j5uZmduzYkeG9Otp32rRpxs3NzYwcOdKsXr3arF692tx///2mTJky5tChQ8YYY/bt22eKFy9uhg4datatW2e2bNlipkyZYu644w5z6dIlh/vk9Bped/1+/+CDD7K8jjc7f3p6utm7d68pU6aM6dWrl+2eOXr0qN11y+we... (line truncated to 2000 chars)
3481:       "text/plain": [
3482:        "<Figure size 800x500 with 1 Axes>"
3483:       ]
3484:      },
3485:      "metadata": {},
3486:      "output_type": "display_data"
3487:     }
3488:    ],
3489:    "source": [
3490:     "plt.figure(figsize=(8,5))\n",
3491:     "\n",
3492:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"vocab_richness\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3493:     "\n",
3494:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"vocab_richness\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3495:     "\n",
3496:     "plt.xlabel(\"Vocabulary Richness\")\n",
3497:     "plt.ylabel(\"Frequency\")\n",
3498:     "plt.title(\"Vocabulary Richness Distribution\")\n",
3499:     "plt.legend()\n",
3500:     "\n",
3501:     "plt.show()"
3502:    ]
3503:   },
3504:   {
3505:    "cell_type": "code",
3506:    "execution_count": 614,
3507:    "id": "242b11d8",
3508:    "metadata": {},
3509:    "outputs": [],
3510:    "source": [
3511:     "def avg_word_length(text):\n",
3512:     "    words = text.split()\n",
3513:     "    if len(words) == 0:\n",
3514:     "        return 0\n",
3515:     "    return np.mean([len(word) for word in words])\n",
3516:     "\n",
3517:     "amazon_df[\"avg_word_len\"] = amazon_df[\"review\"].apply(avg_word_length)"
3518:    ]
3519:   },
3520:   {
3521:    "cell_type": "code",
3522:    "execution_count": 615,
3523:    "id": "9adcc1c9",
3524:    "metadata": {},
3525:    "outputs": [
3526:     {
3527:      "data": {
3528:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAq0AAAHVCAYAAADbxcKaAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAR1VJREFUeJzt3XlcVdX+//E3AoKAguI8z+JsDpVTTjlrWuZA2WB6LdPSspuRebWyNLu3W7euWamhpgkpmvNNTU1NU8u5cMp5AkFAQRnX7w9/7K8nUAHRs4XX8/Hg8fCsvfban33Osd4u1t7bxRhjBAAAANhYAWcXAAAAANwKoRUAAAC2R2gFAACA7RFaAQAAYHuEVgAAANgeoRUAAAC2R2gFAACA7RFaAQAAYHuEVgDIoSlTpqhevXrOLuOOSk1NVUBAgD755JO7etwmTZpo0qRJTjtefjlv4F5CaAVs4Mcff1RAQIBatGihtLQ0Z5djG2vXrlVAQIAWLlyYYVtQUJACAgI0ffr0DNumTJmigIAAHT169I7WFxERofDw8Fv2mzBhggICAhQTE3NH67kd9erV05QpUzK0G2N04MABRUZG5njstm3bKiAgQAEBAapTp47uv/9+PfLII5owYYJ+//33TPc5cOCAzp8/n+1j3eg8buWvx8uN876Rm9WY0/MG8gM3ZxcAQPr888915swZHThwQKtWrVK3bt2cXZItNGzYUAcPHtSyZcvUp08fh22hoaE6ceKEFi9erCFDhjhsCwsL08WLF1W5cuW7WO2NnTt3TgcOHFBKSoqzS7mh8PBwRURE3JGxDx8+rOLFi2v+/PmSpMuXL+vIkSNasGCB6tWrp8GDB2vq1Klyd3e39vntt9/k5+eX7WPl9DxyerycuFmNd7MO4F5DaAWcLDIyUt9//73ef/99ff311/rqq68Irf9f8eLFVb9+ff34448O7SdOnNCff/6pwYMHKzQ0VCkpKXJzu/afs0uXLunXX39Vnz595OLi4oyykQlPT08FBARYr5s2bar+/ftr9uzZeuaZZ+Tp6alPP/3U2l6zZs27Wt/dPt6N2KUOwI5YHgA4WXBwsFxdXTVo0CANGzZMy5Yt07lz56ztq1evVkBAgNatW5dh37179yogIEChoaFWW0JCgv71r3+pQ4cOatCggbp06aLZs2c77Dd79mwFBATowoULmjlzptq1a6fatWtLkjZt2mT9Krd27dpq3LixBg4cqE2bNmU4/p9//qnnnntO9913nzp27KilS5dqy5YtCggI0JYtWxz6ZqWuzLRv394KqenWrl2rQoUKacyYMbp06ZJ27Nhhbfvpp5+UkpKi9u3bW22RkZEKCgpSixYt1KhRIz3++OP64YcfHI4zd+5cBQQE6Pz58woODlb79u1Vu3ZtpaamWsfs2bOnGjVqpMDAwCwtC8iu9evX64knntB9992n+++/X6NHj3b4VfH16ywPHz6sgQMHqlGjRurRo4c2b96cYbzU1FR98sknat26tZo1a6bXX39d8fHx6tatm0aMGCFJOn/+vAICApSamqqvv/7a+uyHDRuWYbysHDO7nn76aXXq1EnTpk3TmTNnrPbM1nZu3bpVTz31lB544AG1bt1aL730ko4dO5al87j+vQsPD9fAgQPVsGFDzZ0794bHS7d//371799fjRo1Uu/evbVx40aH7adPn1ZAQIBCQkIy7Nu5c2eNHDkySzXerI558+apR48eatCggdq0aaNJkyYpPj7e2p7d7wZwTzIAnKpWrVrm6aefNsYYExsba3x8fMykSZOs7VeuXDFFixY1/fv3z7Dvyy+/bDw8PExUVJS1f6NGjUzFihXNrFmzzPbt283nn39uihQpYkaNGmXt9+9//9tIMiNHjjR///vfzebNm83o0aONMcZcvnzZ/PHHH+aPP/4wv//+u1m/fr0ZPHiwKVCggNm4caM1xtGjR03x4sVNkyZNzPLly81P... (line truncated to 2000 chars)
3529:       "text/plain": [
3530:        "<Figure size 800x500 with 1 Axes>"
3531:       ]
3532:      },
3533:      "metadata": {},
3534:      "output_type": "display_data"
3535:     }
3536:    ],
3537:    "source": [
3538:     "plt.figure(figsize=(8,5))\n",
3539:     "\n",
3540:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"avg_word_len\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3541:     "\n",
3542:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"avg_word_len\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3543:     "\n",
3544:     "plt.title(\"Average Word Length Distribution\")\n",
3545:     "plt.xlabel(\"Average Word Length\")\n",
3546:     "plt.legend()\n",
3547:     "\n",
3548:     "plt.show()"
3549:    ]
3550:   },
3551:   {
3552:    "cell_type": "code",
3553:    "execution_count": 616,
3554:    "id": "cdc4b080",
3555:    "metadata": {},
3556:    "outputs": [],
3557:    "source": [
3558:     "def avg_word_length(text):\n",
3559:     "    words = text.split()\n",
3560:     "    if len(words) == 0:\n",
3561:     "        return 0\n",
3562:     "    return np.mean([len(word) for word in words])\n",
3563:     "\n",
3564:     "yelp_sample[\"avg_word_len\"] = yelp_sample[\"review\"].apply(avg_word_length)"
3565:    ]
3566:   },
3567:   {
3568:    "cell_type": "code",
3569:    "execution_count": 617,
3570:    "id": "57253df7",
3571:    "metadata": {},
3572:    "outputs": [
3573:     {
3574:      "data": {
3575:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArYAAAHVCAYAAAAEi7iFAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUdxJREFUeJzt3Xt8z/X///H7zGyMjc0w50MYOeRYTs0hZ6KIVjo4pANF6UBS+pSWdPLp9KmQUjJJzioJmZxDiJEcZsxmm23Mzs/fH35eX+82bPNm22u36+Xyvlx6P1+P1+v1eL3f7+W+156v19vFGGMEAAAAFHLF8rsBAAAAwBkItgAAALAFgi0AAABsgWALAAAAWyDYAgAAwBYItgAAALAFgi0AAABsgWALAAAAWyDYAsB19NZbb6lRo0b53cZ1lZGRoYCAAE2fPv2G7rdFixYKDg7Ot/0VleMGChOCLVBI/PrrrwoICFDbtm2VmZmZ3+0UGKtXr1ZAQIC+//77LMsmTJiggIAAzZgxI8uyt956SwEBATp8+PB17S8qKkr79++/at3kyZMVEBCgM2fOXNd+rkWjRo301ltvZRk3xigsLEzR0dF53nbHjh0VEBCggIAANWzYUK1bt9add96pyZMn66+//sp2nbCwMJ06dSrX+7rccVzNv/fnjOO+nCv1mNfjBoqC4vndAICc+eSTT3TixAmFhYXpxx9/VK9evfK7pQKhadOmOnDggJYtW6YBAwY4LJs/f76OHTumRYsWacSIEQ7LFi5cqLi4ONWsWfMGdnt5kZGRCgsLU3p6en63cln79+9XVFTUddn233//rfLly2vevHmSpLNnz+rQoUNasGCBGjVqpOHDh+vjjz+Wm5ubtc4ff/yhsmXL5npfeT2OvO4vL67U443sAyhsCLZAIRAdHa3FixfrjTfe0BdffKHPP/+cYPv/lS9fXo0bN9avv/7qMH7s2DH9888/Gj58uObPn6/09HQVL37hf3mJiYnavn27BgwYIBcXl/xoG9nw8PBQQECA9bxly5YaPHiwvvrqKz300EPy8PDQBx98YC2vV6/eDe3vRu/vcgpKH0BBxFQEoBCYPXu2XF1dNXToUD3++ONatmyZIiMjreWrVq1SQECA1qxZk2Xd3bt3KyAgQPPnz7fGkpKS9M4776hLly5q0qSJevTooa+++sphva+++koBAQE6ffq0Zs2apU6dOqlBgwaSpNDQUOvPxg0aNFDz5s01ZMgQhYaGZtn/P//8o2HDhqlZs2bq2rWrli5dqo0bNyogIEAbN250qM1JX9np3LmzFWQvWr16tUqWLKkXXnhBiYmJ2rZtm7Xst99+U3p6ujp37myNRUdHa8KECWrbtq1uueUWDRw4UD///LPDfr755hsFBATo1KlTmj17tjp37qwGDRooIyPD2mffvn11yy23KCgoKEdTEHJr7dq1uu+++9SsWTO1bt1a48aNc/iz9KXzPv/++28NGTJEt9xyi/r06aMNGzZk2V5GRoamT5+uDh06qFWrVnr++ed17tw59erVS6NHj5YknTp1SgEBAcrIyNAXX3xhvfePP/54lu3lZJ+59eCDD6pbt2763//+pxMnTljj2c013bRpkx544AHdeuut6tChg5588kkdOXIkR8dx6Wu3f/9+DRkyRE2bNtU333xz2f1dtHfvXg0ePFi33HKL+vfvr/Xr1zssj4iIUEBAgEJCQrKs2717d40ZMyZHPV6pj7lz56pPnz5q0qSJAgMDFRwcrHPnzlnLc/vZAAolA6DAq1+/vnnwwQeNMcbEx8eb0qVLm+DgYGv5+fPnTbly5czgwYOzrPvUU08Zd3d3ExMTY61/yy23mOrVq5svv/zSbN261XzyySfGy8vLjB071lrvvffeM5LMmDFjzHPPPWc2bNhgxo0bZ4wx5uzZs2bfvn1m37595q+//jJr1641w4cPN8WKFTPr16+3tnH48GFTvnx5... (line truncated to 2000 chars)
3576:       "text/plain": [
3577:        "<Figure size 800x500 with 1 Axes>"
3578:       ]
3579:      },
3580:      "metadata": {},
3581:      "output_type": "display_data"
3582:     }
3583:    ],
3584:    "source": [
3585:     "plt.figure(figsize=(8,5))\n",
3586:     "\n",
3587:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"avg_word_len\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3588:     "\n",
3589:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"avg_word_len\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3590:     "\n",
3591:     "plt.title(\"Average Word Length Distribution\")\n",
3592:     "plt.xlabel(\"Average Word Length\")\n",
3593:     "plt.legend()\n",
3594:     "\n",
3595:     "plt.show()"
3596:    ]
3597:   },
3598:   {
3599:    "cell_type": "code",
3600:    "execution_count": 618,
3601:    "id": "e5c984ac",
3602:    "metadata": {},
3603:    "outputs": [
3604:     {
3605:      "data": {
3606:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXd8HGed+P+esr1Jq94tWS5y7yV2ilt6IyEmoRyBEODgaAe/y93BHeTgS79QA8eFNAghIb0X23ES996bLFu9t9Vq+87M8/tjJdmyZFuSJTvh9s1LxDv7zPM8M/vMM8/n+TRJCCFIkiRJkiRJkiRJkiRJkgtAvtQdSJIkSZIkSZIkSZIkyYefpGCRJEmSJEmSJEmSJEmSCyYpWCRJkiRJkiRJkiRJkuSCSQoWSZIkSZIkSZIkSZIkuWCSgkWSJEmSJEmSJEmSJEkumKRgkSRJkiRJkiRJkiRJkgsmKVgkSZIkSZIkSZIkSZLkgkkKFkmSJEmSJEmSJEmSJLlgkoJFkiRJPtTous6zzz7L0aNHR7Xe7u5unn32WWpqaka13qEyVtf1YeNS/w6XkldffZVdu3Zd6m4kSZIkyZCRkpm3kyRJcj7eeOMNVFVl1apV/Y5rmsaLL76IzWbjhhtuGHDe888/T2ZmJkuXLh2zvgUCAVwuF9///vf5zne+M+TzqqurKS8vJx6PU1BQwPjx47Hb7X3fHz16lLKyMv785z/zyU9+ciy6fk5Gel3DoaGhgSNHjhAOh8nOzqaoqIiMjIwxaWukXMrfIRqN8sorr/R9liQJt9vNtGnTyMnJGfP2s7OzufHGG/njH/845m0lSZIkyWigXuoOJEmS5IPPb3/7W9avX09nZycWi6Xv+LZt27jjjjuQJInW1lbS0tL6visvL+f222/nm9/85pgKFsNlzZo13HfffRw7doz58+fjdDo5duwYjY2N3HXXXfz0pz8lNTX1UndzTFm/fj333XcfBw8eZM6cOXi9XhoaGtizZw+LFy/mW9/6Frfeeuul7iYAbreb22+/naKioovedmdnJ3fccQfjx49n1qxZCCGorKxk7969rF69mkcffRSbzTZm7d90003MnTt3zOpPkiRJktEmaQqVJEmS87J8+XLC4TBbt27td/ydd94hPz8fs9nM+vXrB3zXe+4Hhccff5xrr72WefPm0djYyLvvvsurr77K8ePHef7553nrrbeorq6+1N0cU5544glWrlzJ7NmzaWhoYOPGjbz88svs3LmTyspKcnJyeOyxxy51N/vIzc3l2Wef5fLLL79kfbj22mt59tlnee6559i9eze/+93vePrpp7n//vvHtN2HHnqIL37xi2PaRpIkSZKMJknBIkmSJOelVzgYTHhYtWoVixYt6hMkelm/fj2qqnLFFVf0O37o0CFeeeUV3n33XQKBwIC2XnnllT678vr6el577TUOHTrU931XVxdvvfUW69evJxqNDvka6uvr+eIXv8jKlSv53//9X9xud7/vr776ajZu3DgkU6BYLMbmzZt5+eWX2bVrF7quD2jr2WefpbOzs9/xeDzOs88+y7FjxwbUOdLrGg719fXce++9XHvttfzhD38gJSWl3/eFhYU888wzfOMb3xhwrhCC/fv388orr/D+++8TiUT6fd/R0cGzzz5LQ0MDAHv37uXVV1+lsrJy0H4M9f4M5mMxnLaG2v/h8MUvfhGn08mrr7466PfV1dW8/vrrvPXWW7S1tfX77sUXXxwgoPeyY8cOXnzxxb7P5/KxOFcb7733Hu+++26/Y4cOHeLZZ5+lqqqq3/HXXnuNnTt39jtWU1PD2rVrWb9+PS0tLYO2nyRJkiSDIpIkSZLkPBiGIdLS0sTll1/edywcDguLxSL+9Kc/ie9+97ti0qRJ/cpnZmaKyy67rO9YZWWlWLBggXC5XGL58uVi0qRJwuVyid/97nf92kpLSxP33HOPuP/++8W0adPE... (line truncated to 2000 chars)
3607:       "text/plain": [
3608:        "<Figure size 1000x500 with 1 Axes>"
3609:       ]
3610:      },
3611:      "metadata": {},
3612:      "output_type": "display_data"
3613:     }
3614:    ],
3615:    "source": [
3616:     "genuine_text = \" \".join(amazon_df[amazon_df[\"label\"] == 0][\"review\"])\n",
3617:     "\n",
3618:     "wordcloud = WordCloud(\n",
3619:     "    width=800,\n",
3620:     "    height=400,\n",
3621:     "    background_color=\"white\"\n",
3622:     ").generate(genuine_text)\n",
3623:     "\n",
3624:     "plt.figure(figsize=(10,5))\n",
3625:     "plt.imshow(wordcloud)\n",
3626:     "plt.axis(\"off\")\n",
3627:     "plt.title(\"Word Cloud - Genuine Reviews\")\n",
3628:     "plt.show()"
3629:    ]
3630:   },
3631:   {
3632:    "cell_type": "code",
3633:    "execution_count": 619,
3634:    "id": "8a4b1b2d",
3635:    "metadata": {},
3636:    "outputs": [
3637:     {
3638:      "data": {
3639:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsnXd8HOWduJ8p27tWvcuWJffeAWMwpncCIQl3SS7hklwuuVxNLncXksuVXy65lLuUS7gULrTQAoQSMBgMBmPce5Vk9a7V9jYz7++PldYWkmzJlsGQffIx0c68+877zszOvN8uCSEEOXLkyJEjR44cOXLkyHEOyO/1AHLkyJEjR44cOXLkyPH+JydY5MiRI0eOHDly5MiR45zJCRY5cuTIkSNHjhw5cuQ4Z3KCRY4cOXLkyJEjR44cOc6ZnGCRI0eOHDly5MiRI0eOcyYnWOTIkSNHjhw5cuTIkeOcyQkWOXLkyJEjR44cOXLkOGdygkWOHDly5MiRI0eOHDnOmZxgkSNHjncVXdd57LHHOHz48JT2Gw6Heeyxx2hpaZnSfifK+ZpXjguf98u1f+aZZ9ixY8d7PYwcOXJ8gMkJFjlyfAB5/vnn2bBhw6jtmqbx2GOP8eyzz475vSeeeILNmzef17HF43Fuv/12HnvssUl9r7m5mQ0bNvDcc8+xb98+YrHYiP3t7e3cfvvtvPbaa1M53AlztvOaDL/97W957LHHSKfTY+5PJpM89thj7N69e1L9dnR08PLLL/PMM8+wfft2ent7p2C0FxbBYJDHHnuMtra2Ke97otd++PoM/3v88cfZsGEDnZ2dUz6msfj0pz/NT37yk3flWDly5PjDJCdY5MjxAeSHP/whN910E8lkcsT2rVu3cvvtt3PDDTfQ398/Yt/Ro0e57bbbePLJJ9/FkZ6ZDRs2sHjxYmbPns2//uu/8uMf/5hbb72VwsJC7r77bgKBwHs9xHeFzZs3c+utt3L77bfz9NNPj9kmEAhw++2387//+78T6vOVV15h+fLl1NbWcs899/Czn/2Mz372sxQXF3PxxRdfcPfCudDU1MTtt99+3gXn0zF8fb7yla/w8MMP8+CDD/LlL3+ZsrIy7rzzTuLx+Hk9/g033MDSpUvP6zFy5Mjxh01OsMiR4wPI5ZdfTjwe56233hqxfePGjZSXl2M2m3nllVdG7Rv+7oXCfffdx9VXX83SpUvp7Ozk1Vdf5ZlnnuHYsWM88cQTvPDCCzQ3N7/Xw3xX+N///V/Ky8uZP3/+hAWH03H//fdzxRVXsGjRIjo6Oti8eTNPP/0027dvp6mpiZKSEn71q1+d+8BzjOLqq6/OWix27tzJj3/8Y37zm9/wjW9847we99577+Wzn/3seT1Gjhw5/rBR3+sB5MiRY+oZFg5eeeUVLr300uz2jRs3sn79ehobG9m4cSMf+tCHsvteeeUVVFVlzZo1I/o6cOAAjY2NuFwuli5ditPpHLH/d7/7HaWlpSxZsoT29nZ2795NdXU1c+bMATIuKG+99RZms5nVq1dPeA7t7e189rOf5YorruBnP/vZqP1XXnklmzdvRlGUM/aVSqXYvn07fX19lJWVsXDhwhHfa29vZ8uWLaxbtw6fz5fdnk6neeqpp5g3bx719fUj+jzbeZ0NwWCQRx99lK985SsUFRXxuc99jpaWFiorK8+qv/b2du6++26uvvpqfvrTn47aX1lZyaOPPsqmTZtG7RNCsG/fPpqbm/F4PCxfvhyr1ZrdPzAwwMaNG1m9ejWlpaXs3r2btrY25syZQ01NzZjjmWyfe/bsoampiTVr1uByuXjqqaeybS0WC1VVVcybNw9JkoCMq9dLL70EZKx2qpp59c2ePZvZs2dPeBzDTPW1/+xnP8vf/u3f8swzz/D//t//G7W/ubmZAwcOoCgKS5YsIT8/P7vvySefpLi4mJUrV4763rZt22hvb+fmm28GMjEWJSUl... (line truncated to 2000 chars)
3640:       "text/plain": [
3641:        "<Figure size 1000x500 with 1 Axes>"
3642:       ]
3643:      },
3644:      "metadata": {},
3645:      "output_type": "display_data"
3646:     }
3647:    ],
3648:    "source": [
3649:     "fake_text = \" \".join(amazon_df[amazon_df[\"label\"] == 1][\"review\"])\n",
3650:     "\n",
3651:     "wordcloud = WordCloud(\n",
3652:     "    width=800,\n",
3653:     "    height=400,\n",
3654:     "    background_color=\"white\"\n",
3655:     ").generate(fake_text)\n",
3656:     "\n",
3657:     "plt.figure(figsize=(10,5))\n",
3658:     "plt.imshow(wordcloud)\n",
3659:     "plt.axis(\"off\")\n",
3660:     "plt.title(\"Word Cloud - AI Generated Reviews\")\n",
3661:     "plt.show()"
3662:    ]
3663:   },
3664:   {
3665:    "cell_type": "code",
3666:    "execution_count": 620,
3667:    "id": "2b412c33",
3668:    "metadata": {},
3669:    "outputs": [
3670:     {
3671:      "data": {
3672:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXecHFeZqP1UVec8oSdHzYw0yjk5yHKQE7ZxwAZjsmHhLvEue4FluWtzYWGBhV0+wsJ6DRhMtGycg2RLlmUr56yRZjQ5T/f0dO6uqvP90TMttWYk9SjY8m4/v5+t6VNVJ3V11fue8wZJCCHIkSNHjhw5cuTIkSNHjgtAfqc7kCNHjhw5cuTIkSNHjnc/OcUiR44cOXLkyJEjR44cF0xOsciRI0eOHDly5MiRI8cFk1MscuTIkSNHjhw5cuTIccHkFIscOXLkyJEjR44cOXJcMDnFIkeOHDly5MiRI0eOHBdMTrHIkSNHjhw5cuTIkSPHBZNTLHLkyJEjR44cOXLkyHHB5BSLHDlyvKvRNI3Vq1dz5MiRi1pvMBhk9erVtLe3X9R6s+VSjevdxjv9PbyTPP/88+zcufOd7kaOHDlyZI2Uy7ydI0eOc/HSSy9hMBhYtWpVRrmqqjz99NNYrVbe8573jLvuqaeeoqioiKuuuuqS9S0UCuF0OvnWt77FN77xjayva2tro6mpiWQySWVlJXV1ddhstvTxI0eOMH36dH73u9/xoQ996FJ0/ayc77gmQ3d3N4cPHyYajVJSUkJ1dTVer/eStHW+vJPfQzwe57nnnkt/liQJl8vFrFmzKC0tveTtl5SUcNttt/Ff//Vfl7ytHDly5LgYGN7pDuTIkePy56c//Snr16/H7/djNpvT5Vu3buXee+9FkiQGBgYoKChIH2tqauKee+7hy1/+8iVVLCbL2rVr+epXv8rRo0dZvHgxDoeDo0eP0tPTw/3338/3v/998vLy3uluXlLWr1/PV7/6VQ4cOMCCBQvIz8+nu7ub3bt3s3z5cv7+7/+eO++8853uJgAul4t77rmH6urqt71tv9/PvffeS11dHfPmzUMIwYkTJ9izZw/33Xcfv/71r7FarZes/dtvv52FCxdesvpz5MiR42KTM4XKkSPHObnuuuuIRqNs2bIlo3zdunVUVFRgMplYv379uGNj114uPPbYY9x8880sWrSInp4eXn/9dZ5//nmOHTvGU089xSuvvEJbW9s73c1LyuOPP84NN9zA/Pnz6e7u5s033+TZZ59lx44dnDhxgtLSUn7zm9+8091MU1ZWxurVq7n66qvfsT7cfPPNrF69mieffJJdu3bx85//nD//+c9885vfvKTtPvLII3zmM5+5pG3kyJEjx8Ukp1jkyJHjnIwpBxMpD6tWrWLZsmVpRWKM9evXYzAYWLFiRUb5wYMHee6553j99dcJhULj2nruuefSduVdXV288MILHDx4MH08EAjwyiuvsH79euLxeNZj6Orq4jOf+Qw33HAD//mf/4nL5co4fuONN/Lmm29mZQqUSCTYtGkTzz77LDt37kTTtHFtrV69Gr/fn1GeTCZZvXo1R48eHVfn+Y5rMnR1dfGpT32Km2++mV/+8pd4PJ6M41VVVTzxxBP87//9v8ddK4Rg3759PPfcc7zxxhvEYrGM4z6fj9WrV9Pd3Q3Anj17eP755zlx4sSE/ch2fibysZhMW9n2fzJ85jOfweFw8Pzzz094vK2tjRdffJFXXnmFwcHBjGNPP/30OAV9jO3bt/P000+nP5/Nx+JsbWzYsIHXX389o+zgwYOsXr2a1tbWjPIXXniBHTt2ZJS1t7fz6quvsn79evr7+ydsP0eOHDkmROTIkSPHOdB1XRQUFIirr746XRaNRoXZbBa//e1vxUMPPSSmTZuWcX5RUZG44oor0mUnTpwQS5YsEU6nU1x33XVi2rRpwul0ip///OcZbRUUFIgHH3xQfPOb... (line truncated to 2000 chars)
3673:       "text/plain": [
3674:        "<Figure size 1000x500 with 1 Axes>"
3675:       ]
3676:      },
3677:      "metadata": {},
3678:      "output_type": "display_data"
3679:     }
3680:    ],
3681:    "source": [
3682:     "genuine_text = \" \".join(yelp_sample[yelp_sample[\"label\"] == 0][\"review\"])\n",
3683:     "\n",
3684:     "wordcloud = WordCloud(\n",
3685:     "    width=800,\n",
3686:     "    height=400,\n",
3687:     "    background_color=\"white\"\n",
3688:     ").generate(genuine_text)\n",
3689:     "\n",
3690:     "plt.figure(figsize=(10,5))\n",
3691:     "plt.imshow(wordcloud)\n",
3692:     "plt.axis(\"off\")\n",
3693:     "plt.title(\"Word Cloud - Genuine Reviews\")\n",
3694:     "plt.show()"
3695:    ]
3696:   },
3697:   {
3698:    "cell_type": "code",
3699:    "execution_count": 621,
3700:    "id": "8e53a10b",
3701:    "metadata": {},
3702:    "outputs": [
3703:     {
3704:      "data": {
3705:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsnXd8HNW5sJ8p24t6r5Yly70XsI0LtsH0akpCAgmQkEKSW5Jwc3MDhNRLGt9NhUAg9I4B0wwuYHDv3bItq/eyK22fmfP9sdLaa8m25AI22ef3ky2dmTll6nnP2yQhhCBBggQJEiRIkCBBggQJTgH5s+5AggQJEiRIkCBBggQJzn0SgkWCBAkSJEiQIEGCBAlOmYRgkSBBggQJEiRIkCBBglMmIVgkSJAgQYIECRIkSJDglEkIFgkSJEiQIEGCBAkSJDhlEoJFggQJEiRIkCBBggQJTpmEYJEgQYIECRIkSJAgQYJTJiFYJEiQIEGCBAkSJEiQ4JRJCBYJEiT4VNF1nZdeeok9e/ac1nq7urp46aWXqK6uPq31DpQzNa4EZz/nyrV/88032bhx42fdjQQJEnyOSQgWCRJ8Dnn77bdZunRpn3JN03jppZdYsmRJv8e98sorrFq16oz2LRAIsGjRIl566aVBHVdVVcXSpUt566232L59O36/P257XV0dixYt4sMPPzyd3R0wJzuuwfDqq6/y0ksvEYlE+t0eCoV46aWX2LJly6Dqra+v54MPPuDNN99kw4YNtLS0nIbenl14PB5eeuklamtrT3vdA732vden9+fll19m6dKlNDQ0nPY+9ccdd9zBX/7yl0+lrQQJEvxrkhAsEiT4HPLHP/6Rq666ilAoFFe+du1aFi1axBVXXEFbW1vctn379nHdddfx2muvfYo9PTFLly5l4sSJjBw5kp///Of8+c9/5tprryUzM5M777yTjo6Oz7qLnwqrVq3i2muvZdGiRbz++uv97tPR0cGiRYv4+9//PqA6ly9fztSpUyktLeXee+/l4Ycf5q677iI7O5uZM2eedffCqVBZWcmiRYvOuOB8PHqvzz333MNzzz3HM888ww9/+EPy8vK46aabCAQCZ7T9K664gsmTJ5/RNhIkSPCvTUKwSJDgc8iFF15IIBBgzZo1ceXLli0jPz8fs9nM8uXL+2zrPfZs4YknnmDhwoVMnjyZhoYGVqxYwZtvvklFRQWvvPIK7777LlVVVZ91Nz8V/v73v5Ofn8/YsWMHLDgcj6eeeor58+czYcIE6uvrWbVqFa+//jobNmygsrKSnJwcHn/88VPveII+LFy4MKax2LRpE3/+8595/vnnuf/++89ou4888gh33XXXGW0jQYIE/9qon3UHEiRIcPrpFQ6WL1/O7NmzY+XLli1jwYIFHDx4kGXLlnH99dfHti1fvhxVVZk1a1ZcXTt37uTgwYO4XC4mT56M0+mM2/7GG2+Qm5vLpEmTqKurY8uWLRQXFzNq1CggaoKyZs0azGYz06dPH/AY6urquOuuu5g/fz4PP/xwn+0XXXQRq1atQlGUE9YVDofZsGEDra2t5OXlMX78+Ljj6urqWL16NfPmzSMlJSVWHolEWLx4MWPGjKG8vDyuzpMd18ng8Xh48cUXueeee8jKyuIb3/gG1dXVFBYWnlR9dXV13HnnnSxcuJC//e1vfbYXFhby4osvsnLlyj7bhBBs376dqqoqkpKSmDp1KlarNba9vb2dZcuWMX36dHJzc9myZQu1tbWMGjWKIUOG9Nufwda5detWKisrmTVrFi6Xi8WLF8f2tVgsFBUVMWbMGCRJAqKmXu+//z4Q1dqpavTTN3LkSEaOHDngfvRyuq/9XXfdxfe//33efPNNfvWrX/XZXlVVxc6dO1EUhUmTJpGenh7b9tprr5Gdnc15553X57j169dTV1fH1VdfDUR9LHJycpg0adKg2li5ciVCCObMmRMr27lzJ7t3... (line truncated to 2000 chars)
3706:       "text/plain": [
3707:        "<Figure size 1000x500 with 1 Axes>"
3708:       ]
3709:      },
3710:      "metadata": {},
3711:      "output_type": "display_data"
3712:     }
3713:    ],
3714:    "source": [
3715:     "fake_text = \" \".join(yelp_sample[yelp_sample[\"label\"] == 1][\"review\"])\n",
3716:     "\n",
3717:     "wordcloud = WordCloud(\n",
3718:     "    width=800,\n",
3719:     "    height=400,\n",
3720:     "    background_color=\"white\"\n",
3721:     ").generate(fake_text)\n",
3722:     "\n",
3723:     "plt.figure(figsize=(10,5))\n",
3724:     "plt.imshow(wordcloud)\n",
3725:     "plt.axis(\"off\")\n",
3726:     "plt.title(\"Word Cloud - AI Generated Reviews\")\n",
3727:     "plt.show()"
3728:    ]
3729:   },
3730:   {
3731:    "cell_type": "code",
3732:    "execution_count": 622,
3733:    "id": "9e4c4ec4",
3734:    "metadata": {},
3735:    "outputs": [],
3736:    "source": [
3737:     "def plot_top_words(dataframe, label, title):\n",
3738:     "    vectorizer = CountVectorizer(stop_words=\"english\", max_features=20)\n",
3739:     "\n",
3740:     "    X = vectorizer.fit_transform(dataframe[dataframe[\"label\"] == label][\"review\"])\n",
3741:     "\n",
3742:     "    counts = np.asarray(X.sum(axis=0)).flatten()\n",
3743:     "\n",
3744:     "    words = vectorizer.get_feature_names_out()\n",
3745:     "\n",
3746:     "    pairs = sorted(zip(words, counts), key=lambda x: x[1], reverse=True)\n",
3747:     "\n",
3748:     "    words, counts = zip(*pairs)\n",
3749:     "\n",
3750:     "    plt.figure(figsize=(8,6))\n",
3751:     "    plt.barh(words, counts)\n",
3752:     "    plt.title(title)\n",
3753:     "    plt.xlabel(\"Frequency\")\n",
3754:     "    plt.gca().invert_yaxis()\n",
3755:     "    plt.show()"
3756:    ]
3757:   },
3758:   {
3759:    "cell_type": "code",
3760:    "execution_count": 623,
3761:    "id": "ae6776f1",
3762:    "metadata": {},
3763:    "outputs": [
3764:     {
3765:      "data": {
3766:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsYAAAIiCAYAAADLvQ4hAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAdHhJREFUeJzt3XdUVEfDBvCHpSxFutJkRQVF7LGBHSsaLCjGbixYYkk0MeYNxhJLgulqEhONXTFGjQK2WMGosceuqIAURQ0i7ALK0ub7g48bN6ABA+wCz++cPcc7d+7M3MXyZDJ3rp4QQoCIiIiIqIqTaXsARERERES6gMGYiIiIiAgMxkREREREABiMiYiIiIgAMBgTEREREQFgMCYiIiIiAsBgTEREREQEgMGYiIiIiAgAgzERUanLycnB6tWrcenSpf/cllKpxOrVqxEdHf3fB1aBVeXvYcuWLThx4oS2h0FUJejxzXdEFd/BgwcRHx//r/Xs7OzQr1+/Mh9PSkoKLl68iEePHsHFxQUtWrSAsbHxC+tHRUXh/PnzMDAwQPv27eHo6Pivffzyyy8wMDCAv7+/RnlWVhY2btwIU1NTDB8+vNB1a9euRc2aNeHj41PyGyum9PR0mJubY9GiRZgzZ85/aisyMhIeHh7YtGkTRo4cWUoj/JsQAjdv3sTNmzfx7NkzODg4oHbt2nBzcyv1vv6Lsv4eXubZs2cIDg6WjvX09GBhYYGmTZvC3d29zPt3cHBAnz59sHr16jLvi6iqM9D2AIjov7t16xYuX74sHcfFxeHw4cPo1KkT6tWrJ5W7urqWaTBOTU3FlClTsHPnTjRt2hRubm44d+4cMjMz8e2338LPz0+jfl5eHqZOnYr169ejd+/eePbsGUaOHIlPPvkEM2fOfGlfW7ZswYEDB/D666/DxMREKj916hQmTJgAAOjWrRvs7e2lc9evX0dAQAD+97//lWkwLk1WVlYICAgok6AaGhqKDz74AElJSWjXrh1sbGyQmJiI48ePo169eggMDMSIESNKvd9XUZbfw79RKpWYMGECGjZsiLZt20IIgbt37yIiIgI9e/bE9u3bYW5uXmb9jxgxAk2bNi2z9onoOYKIKp1du3YJAGLdunXl2u/NmzeFo6OjOHjwoFSWnZ0thgwZIgwMDMS1a9c06n/xxRdCJpOJY8eOSWWrV68WAMT+/ftf2tfSpUsFAHH48GGN8nnz5onatWsLU1NT8fPPP2uc+/bbbwUAceDAgVe9xWJJS0sTAMSiRYvKtJ//YsWKFQKAmDVrlnj69KnGucePH4uAgADh5+enpdHplgcPHggAYurUqRrlwcHBAoCYPn26dgZGRKWOa4yJqpDc3FycOHECmzZtQkhICJKSkgrV2bRpE06ePAkAuHz5MoKDgxEeHo7c3Nx/bd/W1hanT59Gjx49pDIDAwPMmjULOTk5+PXXX6XyvLw8fP311+jWrRs6deoklY8bNw4uLi744osvXtpX165dAQBHjx7VKD969Ch69OiBtm3bFnnOyMgIHTp0kMpyc3Nx8uRJ6Tv566+/CvW1efNmaY1nZGQkgoODceHCBen8gwcP8Msvv2DXrl1QqVQvHHNeXh5OnjyJn3/+GQcOHCjy+/+notbWJiUlYfXq1YiLi4MQAhEREdi8eXOx1zTHxsZi+vTp8Pf3x+eff64x4w7k/xxXr16Njz76qNC12dnZ+P3337Fp0yaEhYUhJSVF43xJxhYbG4vVq1fj8ePHGuVZWVlYvXo1rly5Uurfw7+NvySGDx8OCwsLHDhwoMjzly9fxpYtW/DLL78gNjZW49zGjRtx+PDhIq8LDw/Hhg0bpOOXrTF+WR/79u3D7t27NcrOnz+P1atX49atWxrlwcHBOH78uEbZtWvXsGPHDuzatatKru2mKkrLwZyIykBRM8bXr18X7u7uws7OTvj7+4vWrVsLuVwuPvvsM41rLS0txaRJk8Tk... (line truncated to 2000 chars)
3767:       "text/plain": [
3768:        "<Figure size 800x600 with 1 Axes>"
3769:       ]
3770:      },
3771:      "metadata": {},
3772:      "output_type": "display_data"
3773:     },
3774:     {
3775:      "data": {
3776:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAvYAAAIiCAYAAACjTowZAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAfYBJREFUeJzt3XdUVMfbB/AvS1kEKYJ0EEQExQJRY8UuKsHeayxYYmKsPxMxMUZjgqaYGGMSY4/R2BtqxIItiIrGrqCCFEUU266iLLDM+4cvN64UIYIru9/POXsOd+7cuc/cXeDZ2bmzBkIIASIiIiIiKtdk2g6AiIiIiIheHRN7IiIiIiIdwMSeiIiIiEgHMLEnIiIiItIBTOyJiIiIiHQAE3siIiIiIh3AxJ6IiIiISAcwsSciIiIi0gFM7ImItCwnJwdLlizBmTNnXrkthUKBJUuWID4+/tUDo3KlNF9HZWnNmjX4+++/tR0GkU4y4DfPEumfPXv2IDk5+aX17O3t0aVLlzKP58GDBzh9+jRu374Nd3d31KtXD6ampoXWv3btGk6ePAkjIyM0a9YMTk5OLz3HunXrYGRkhJ49e2qUZ2Vl4ffff4eZmRkGDBiQ77hly5bBxcUFHTp0KHnHiunx48ewsLDAF198gU8//fSV2oqNjUXNmjWxatUqDBo0qJQi/JcQAitWrIBarcbgwYMhl8vz1Xn69ClWr16NWrVqoUmTJsVu9/Lly7h8+TKePn0KR0dHeHh4wMvLq7S7oFX379/H5s2b0aZNG3h6epZq28V9HeU9P3kMDAxgaWmJunXrwsfHp1RjKoijoyM6deqEJUuWlPm5iPSNkbYDIKLXLy4uDmfPnpW2k5KSsG/fPrRo0QLVq1eXyqtVq1amif3Dhw/x/vvvY/Pmzahbty68vLwQExODzMxMLFiwAN26ddOon5ubiw8++AArVqxAUFAQnj59ikGDBuHLL7/E5MmTizzXmjVrEBERgXfeeQcVKlSQyqOjozFy5EgAQNu2beHg4CDtu3jxIkJCQvDxxx+XaWJfmqytrRESElJmCfGBAwcwfPhwAIC5uTn69++fr45CocDIkSPxwQcfFCux37ZtGz766COkp6ejadOmsLGxQWpqKo4cOYLq1asjNDQUAwcOLPW+aENycjJGjhyJP//8s9QT++LKe358fX3RpEkTCCFw/fp1HDx4EO3bt8eGDRtgYWFRZucfOHAg6tatW2btE+k1QUR6b8uWLQKAWL58+Ws97+XLl4WTk5PYs2ePVJadnS369u0rjIyMxIULFzTqf/PNN0Imk4lDhw5JZUuWLBEAxF9//VXkuX744QcBQOzbt0+j/LPPPhMeHh7CzMxM/Pnnnxr7FixYIACIiIiI/9rFYnn06JEAIL744osyPU9p6N+/v6hatap4++23RZs2bQqsc+vWLQFAfPDBBy9t7+effxYAxJQpU8STJ0809t29e1eEhISIbt26lUrsb4LTp08LAPlea6WhuK+jwp6f1atXCwBi/PjxpR4bEb0eHLEnokKp1WpER0fj+vXrsLCwQLNmzWBnZ6dRZ9WqVfD09ESzZs1w9uxZXLhwAc7OzmjRogUMDQ2LbN/W1hbHjh1DlSpVpDIjIyNMmTIF69atw6ZNm1CrVi0Az0br582bh7Zt26JFixZS/eHDh+OLL77AN998g44dOxZ6rjZt2gAAIiMj0bZtW6k8MjISgYGBSEhIQGRkJPr166exz8TEBAEBARrX5NixY0hISICFhQWaNm0Ke3t7jXP98ccf8PDwQEBAAGJjY3Hq1CnUqFED9evXBwDcunULhw8fhomJCdq2bQuZrODbnXJzcxEdHY3k5GTY2NigXr16+a7/ixQKBTZs2IDWrVujWrVqAID09HRs27YNgYGBqFKlCg4dOoQbN26gdu3a8Pf3L7K95+VNI5k5cyYcHBwwfPhwxMfHS+cpqcTERIwfPx49e/bE119/... (line truncated to 2000 chars)
3777:       "text/plain": [
3778:        "<Figure size 800x600 with 1 Axes>"
3779:       ]
3780:      },
3781:      "metadata": {},
3782:      "output_type": "display_data"
3783:     }
3784:    ],
3785:    "source": [
3786:     "plot_top_words(amazon_df, 0, \"Top 20 Words in Genuine Reviews\")\n",
3787:     "\n",
3788:     "plot_top_words(amazon_df, 1, \"Top 20 Words in AI Generated Reviews\")"
3789:    ]
3790:   },
3791:   {
3792:    "cell_type": "code",
3793:    "execution_count": 624,
3794:    "id": "93bfa8fb",
3795:    "metadata": {},
3796:    "outputs": [
3797:     {
3798:      "data": {
3799:       "text/html": [
3800:        "<div>\n",
3801:        "<style scoped>\n",
3802:        "    .dataframe tbody tr th:only-of-type {\n",
3803:        "        vertical-align: middle;\n",
3804:        "    }\n",
3805:        "\n",
3806:        "    .dataframe tbody tr th {\n",
3807:        "        vertical-align: top;\n",
3808:        "    }\n",
3809:        "\n",
3810:        "    .dataframe thead th {\n",
3811:        "        text-align: right;\n",
3812:        "    }\n",
3813:        "</style>\n",
3814:        "<table border=\"1\" class=\"dataframe\">\n",
3815:        "  <thead>\n",
3816:        "    <tr style=\"text-align: right;\">\n",
3817:        "      <th></th>\n",
3818:        "      <th>review</th>\n",
3819:        "      <th>label</th>\n",
3820:        "      <th>word_count</th>\n",
3821:        "    </tr>\n",
3822:        "  </thead>\n",
3823:        "  <tbody>\n",
3824:        "    <tr>\n",
3825:        "      <th>25740</th>\n",

(Output capped at 50 KB. Showing lines 3082-3825. Use offset=3826 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 5.8s)

_Thinking:_

Let me finish reading the rest of the notebook.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 3826
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
3826:        "      <td>i enjoyed this werewolf story the heroine is a wonderful character and her son s are sure to be strong characters in future books the hero is a well rounded character as well and i look forward to...</td>\n",
3827:        "      <td>0</td>\n",
3828:        "      <td>49</td>\n",
3829:        "    </tr>\n",
3830:        "    <tr>\n",
3831:        "      <th>24464</th>\n",
3832:        "      <td>i enjoyed the story i loved the characters i loved the history i enjoyed the way the author portrayed the characters</td>\n",
3833:        "      <td>1</td>\n",
3834:        "      <td>21</td>\n",
3835:        "    </tr>\n",
3836:        "    <tr>\n",
3837:        "      <th>15012</th>\n",
3838:        "      <td>this is a terrfic series that has the characters and plots of a science fiction story it has the appearance of a very dark and disturbing world the characters are not the same as the original movi...</td>\n",
3839:        "      <td>1</td>\n",
3840:        "      <td>155</td>\n",
3841:        "    </tr>\n",
3842:        "    <tr>\n",
3843:        "      <th>31165</th>\n",
3844:        "      <td>rick bragg is one of the most entertaining characters i ve read in a long time this is a very well written book and i am sure you ll enjoy it as much as i do it s a very well written story and i m...</td>\n",
3845:        "      <td>1</td>\n",
3846:        "      <td>68</td>\n",
3847:        "    </tr>\n",
3848:        "    <tr>\n",
3849:        "      <th>27064</th>\n",
3850:        "      <td>very good book and for a beginner the writing is good there is a lot of detail and so on i liked how the characters were developed the story line was interesting and the characters were well devel...</td>\n",
3851:        "      <td>1</td>\n",
3852:        "      <td>89</td>\n",
3853:        "    </tr>\n",
3854:        "    <tr>\n",
3855:        "      <th>15028</th>\n",
3856:        "      <td>this movie is available in both english and french which is a nice bonus i recommend it i really enjoyed the movie the characters and the story were great the acting was great the acting was great...</td>\n",
3857:        "      <td>1</td>\n",
3858:        "      <td>141</td>\n",
3859:        "    </tr>\n",
3860:        "    <tr>\n",
3861:        "      <th>15283</th>\n",
3862:        "      <td>dirty harry is more than a little predictable the two main characters are just too predictable and predictable the movie is also a bit too long and the first half is pretty straight forward the se...</td>\n",
3863:        "      <td>1</td>\n",
3864:        "      <td>201</td>\n",
3865:        "    </tr>\n",
3866:        "    <tr>\n",
3867:        "      <th>26227</th>\n",
3868:        "      <td>no one includes a better mix of action adventure romance and humor in one story than patti larsen and this installment of the blood gold series is no different i love larsen s writing and characte...</td>\n",
3869:        "      <td>0</td>\n",
3870:        "      <td>64</td>\n",
3871:        "    </tr>\n",
3872:        "    <tr>\n",
3873:        "      <th>24942</th>\n",
3874:        "      <td>i have enjoyed this author s work the characters are well developed and the story is well told the story is well written the characters are well</td>\n",
3875:        "      <td>1</td>\n",
3876:        "      <td>27</td>\n",
3877:        "    </tr>\n",
3878:        "    <tr>\n",
3879:        "      <th>25639</th>\n",
3880:        "      <td>wow this was an awesome book the characters were well developed and i enjoyed the story the writing is well done the story is well told and the flow of the story is well developed the author does ...</td>\n",
3881:        "      <td>1</td>\n",
3882:        "      <td>42</td>\n",
3883:        "    </tr>\n",
3884:        "  </tbody>\n",
3885:        "</table>\n",
3886:        "</div>"
3887:       ],
3888:       "text/plain": [
3889:        "                                                                                                                                                                                                        review  \\\n",
3890:        "25740  i enjoyed this werewolf story the heroine is a wonderful character and her son s are sure to be strong characters in future books the hero is a well rounded character as well and i look forward to...   \n",
3891:        "24464                                                                                     i enjoyed the story i loved the characters i loved the history i enjoyed the way the author portrayed the characters   \n",
3892:        "15012  this is a terrfic series that has the characters and plots of a science fiction story it has the appearance of a very dark and disturbing world the characters are not the same as the original movi...   \n",
3893:        "31165  rick bragg is one of the most entertaining characters i ve read in a long time this is a very well written book and i am sure you ll enjoy it as much as i do it s a very well written story and i m...   \n",
3894:        "27064  very good book and for a beginner the writing is good there is a lot of detail and so on i liked how the characters were developed the story line was interesting and the characters were well devel...   \n",
3895:        "15028  this movie is available in both english and french which is a nice bonus i recommend it i really enjoyed the movie the characters and the story were great the acting was great the acting was great...   \n",
3896:        "15283  dirty harry is more than a little predictable the two main characters are just too predictable and predictable the movie is also a bit too long and the first half is pretty straight forward the se...   \n",
3897:        "26227  no one includes a better mix of action adventure romance and humor in one story than patti larsen and this installment of the blood gold series is no different i love larsen s writing and characte...   \n",
3898:        "24942                                                         i have enjoyed this author s work the characters are well developed and the story is well told the story is well written the characters are well   \n",
3899:        "25639  wow this was an awesome book the characters were well developed and i enjoyed the story the writing is well done the story is well told and the flow of the story is well developed the author does ...   \n",
3900:        "\n",
3901:        "       label  word_count  \n",
3902:        "25740      0          49  \n",
3903:        "24464      1          21  \n",
3904:        "15012      1         155  \n",
3905:        "31165      1          68  \n",
3906:        "27064      1          89  \n",
3907:        "15028      1         141  \n",
3908:        "15283      1         201  \n",
3909:        "26227      0          64  \n",
3910:        "24942      1          27  \n",
3911:        "25639      1          42  "
3912:       ]
3913:      },
3914:      "execution_count": 624,
3915:      "metadata": {},
3916:      "output_type": "execute_result"
3917:     }
3918:    ],
3919:    "source": [
3920:     "amazon_df[\n",
3921:     "    amazon_df[\"review\"].str.contains(r\"\\bcharacters\\b\", case=False, na=False)\n",
3922:     "][[\"review\", \"label\", \"word_count\"]].sample(10, random_state=42)"
3923:    ]
3924:   },
3925:   {
3926:    "cell_type": "code",
3927:    "execution_count": 625,
3928:    "id": "355048a8",
3929:    "metadata": {},
3930:    "outputs": [
3931:     {
3932:      "name": "stdout",
3933:      "output_type": "stream",
3934:      "text": [
3935:       "Label Distribution:\n",
3936:       "label\n",
3937:       "0    1130\n",
3938:       "1    2567\n",
3939:       "Name: count, dtype: int64\n",
3940:       "\n",
3941:       "Percentage Distribution:\n",
3942:       "label\n",
3943:       "0    30.57\n",
3944:       "1    69.43\n",
3945:       "Name: count, dtype: float64\n"
3946:      ]
3947:     }
3948:    ],
3949:    "source": [
3950:     "# Reviews containing the word \"characters\"\n",
3951:     "characters_reviews = amazon_df[\n",
3952:     "    amazon_df[\"review\"].str.contains(r\"\\bcharacters\\b\", case=False, na=False)\n",
3953:     "]\n",
3954:     "\n",
3955:     "# Count of Genuine (0) and AI Generated (1)\n",
3956:     "label_counts = characters_reviews[\"label\"].value_counts().sort_index()\n",
3957:     "\n",
3958:     "print(\"Label Distribution:\")\n",
3959:     "print(label_counts)\n",
3960:     "\n",
3961:     "print(\"\\nPercentage Distribution:\")\n",
3962:     "print((label_counts / len(characters_reviews) * 100).round(2))"
3963:    ]
3964:   },
3965:   {
3966:    "cell_type": "code",
3967:    "execution_count": 626,
3968:    "id": "c65b48d6",
3969:    "metadata": {},
3970:    "outputs": [
3971:     {
3972:      "name": "stdout",
3973:      "output_type": "stream",
3974:      "text": [
3975:       "Label Distribution:\n",
3976:       "label\n",
3977:       "0    1373\n",
3978:       "1    3424\n",
3979:       "Name: count, dtype: int64\n",
3980:       "\n",
3981:       "Percentage Distribution:\n",
3982:       "label\n",
3983:       "0    28.62\n",
3984:       "1    71.38\n",
3985:       "Name: count, dtype: float64\n"
3986:      ]
3987:     }
3988:    ],
3989:    "source": [
3990:     "# Reviews containing the word \"recommend\"\n",
3991:     "recommend_reviews = amazon_df[\n",
3992:     "    amazon_df[\"review\"].str.contains(r\"\\brecommend\\b\", case=False, na=False)\n",
3993:     "]\n",
3994:     "\n",
3995:     "# Count of Genuine (0) and AI Generated (1)\n",
3996:     "label_counts = recommend_reviews[\"label\"].value_counts().sort_index()\n",
3997:     "\n",
3998:     "print(\"Label Distribution:\")\n",
3999:     "print(label_counts)\n",
4000:     "\n",
4001:     "print(\"\\nPercentage Distribution:\")\n",
4002:     "print((label_counts / len(recommend_reviews) * 100).round(2))"
4003:    ]
4004:   },
4005:   {
4006:    "cell_type": "markdown",
4007:    "id": "8a8d80d3",
4008:    "metadata": {},
4009:    "source": [
4010:     "These 2 words recommend and characters where very prominently used by AI to write the review on the other hand humans didn't use these words as much."
4011:    ]
4012:   },
4013:   {
4014:    "cell_type": "markdown",
4015:    "id": "b0841ec0",
4016:    "metadata": {},
4017:    "source": [
4018:     "Side Note: - This also tells us one thing without checking the category in which fake reviews are more common than the others. Since, \"characters\" word were used so often by AI its safe to say AI generated reviews are very common in books category."
4019:    ]
4020:   },
4021:   {
4022:    "cell_type": "code",
4023:    "execution_count": 627,
4024:    "id": "bf66d309",
4025:    "metadata": {},
4026:    "outputs": [
4027:     {
4028:      "data": {
4029:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAtUAAAIiCAYAAAAHJDTKAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAfhtJREFUeJzt3XdYFNf7NvB7aYsgXRHQFZVmw4LdWECxICoqWGIwaqxRk/A10QRj1wQ1iSYmGhN7jyX23mussYKKooIYRQWBVaRz3j98mZ8rxcUFFpb7c117xTnzzJxnJogPhzNnZEIIASIiIiIiem962k6AiIiIiKi0Y1FNRERERKQhFtVERERERBpiUU1EREREpCEW1UREREREGmJRTURERESkIRbVREREREQaYlFNRERERKQhFtVERCVYRkYGlixZgitXrmh8rsTERCxZsgR3797VPLFSrCzfh3Xr1uHUqVPaToNIJ8n4RkUietOBAwfw4MGDd8bZ2tqie/fuRZ5PfHw8Ll++jCdPnsDR0REeHh4wNjbOMz4iIgIXL16EgYEBPvjgA9jb27+zjw0bNsDAwAD+/v4q7WlpaVi1ahVMTEzQv3//HMctW7YMlStXRqdOnQp+YWp6+fIlzMzMMGPGDEycOFGjc926dQu1atXC6tWrERgYWEgZ/h8hBG7evImbN28iOTkZdnZ2qFatGpydnQu9L00U9X3IT3JyMtauXStty2QymJubo169enBzcyvy/u3s7NC1a1csWbKkyPsiKmsMtJ0AEZUs4eHhuHr1qrQdFRWFQ4cOoU2bNnBxcZHanZycirSoTkhIwKhRo7BlyxbUq1cPzs7OuHDhAlJSUvDrr7+iR48eKvFZWVkYPXo0VqxYAR8fHyQnJyMwMBDfffcdvvzyy3z7WrduHfbv348uXbqgXLlyUvuZM2cwbNgwAED79u1RqVIlaV9YWBiGDBmCr7/+ukiL6sJkaWmJIUOGFEmRu337dowfPx7Pnj1Dy5YtYW1tjUePHuHkyZNwcXFBcHAwPvroo0Lv930U5X14l8TERAwbNgy1a9dGixYtIITA/fv3cezYMXTs2BGbNm2CmZlZkfX/0UcfoV69ekV2fqIyTRAR5WPr1q0CgFi+fHmx9nvz5k1hb28vDhw4ILWlp6eLvn37CgMDAxEaGqoS/8MPPwg9PT1x/PhxqW3JkiUCgNi7d2++ff38888CgDh06JBK++TJk0W1atWEiYmJWL9+vcq+X3/9VQAQ+/fvf99LVMuLFy8EADFjxowi7UcTCxcuFADEuHHjxKtXr1T2xcbGiiFDhogePXpoKbuS5fHjxwKAGD16tEr72rVrBQDxxRdfaCcxItIY51QT0XvJzMzEqVOnsHr1amzbtg3Pnj3LEbN69WqcPn0aAHD16lWsXbsWR48eRWZm5jvPb2Njg7Nnz6JDhw5Sm4GBAcaNG4eMjAz8/fffUntWVhbmzp2L9u3bo02bNlL7J598AkdHR/zwww/59tWuXTsAwJEjR1Tajxw5gg4dOqBFixa57jMyMkKrVq2ktszMTJw+fVq6J0+fPs3R15o1a6Q5rbdu3cLatWvx77//SvsfP36MDRs2YOvWrVAqlXnmnJWVhdOnT2P9+vXYv39/rvf/bbnNJX727BmWLFmCqKgoCCFw7NgxrFmzRu053JGRkfjiiy/g7++POXPmqIz0A6//Py5ZsgTffvttjmPT09Nx4sQJrF69Gjt27EB8fLzK/oLkFhkZiSVLliA2NlalPS0tDUuWLMG1a9cK/T68K/+C6N+/P8zNzbF///5c91+9ehXr1q3Dhg0bEBkZqbJv1apVOHToUK7HHT16FCtXrpS285tTnV8fe/bswc6dO1XaLl68iCVLliA8PFylfe3atTh58qRKW2hoKDZv3oytW7eWybnsVEZouagnohIut5HqsLAw4ebmJmxtbYW/v79o0qSJkMvlYvbs2SrHWlhYiBEj... (line truncated to 2000 chars)
4030:       "text/plain": [
4031:        "<Figure size 800x600 with 1 Axes>"
4032:       ]
4033:      },
4034:      "metadata": {},
4035:      "output_type": "display_data"
4036:     },
4037:     {
4038:      "data": {
4039:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAtYAAAIiCAYAAADsE4/JAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAgTlJREFUeJzs3XdUFNfbB/AvdZG2gFIUEEREUVBEImJFxajBhlhji7HFxCTG5KchGo2aBE2i0WiqvWBssffesbeIiIIFFDGiworCAst9//Awb1aKS1xYWL6fc/Yc584zd54ZV3283LljIIQQICIiIiKi12Ko6wSIiIiIiPQBC2siIiIiIi1gYU1EREREpAUsrImIiIiItICFNRERERGRFrCwJiIiIiLSAhbWRERERERawMKaiIiIiEgLWFgTEWlRbm4uFi5ciIsXL752X+np6Vi4cCESEhJePzGqULT5PSpNq1atwrFjx3SdBlG5YcA3LxJVbHv27EFiYuIr4xwcHNCtW7dSz+fJkye4cOECHjx4ADc3N/j7+8PMzKzI+Pj4eJw9exbGxsZo0aIFqlev/spzrFmzBsbGxggPD1drz87OxvLly2Fubo633367wHGLFy+Gs7MzOnbsWPIL01BGRgasrKwwffp0TJo06bX6unbtGry9vbFixQoMHDhQSxn+PyEEli5dCpVKhUGDBkEmkxWIyczMRFRUFBo0aICgoCCN+42NjUVsbCwyMzPh5OQEd3d3eHp6avsSdOrx48fYsGED2rVrBw8PD632ren3KP/3J5+BgQGsra3RsGFD1K1bV6s5FcbJyQldunTBwoULS/1cRBWBsa4TIKLXExcXh0uXLknbd+7cwb59+9C6dWvUqVNHaq9du3apFtZpaWl4//33sWHDBjRs2BCenp44c+YMsrKyMG/ePPTo0UMtPi8vDx988AGWLl2Kzp07IzMzEwMHDsQ333yDTz/9tNhzrVq1Crt378Zbb72FKlWqSO3R0dEYMWIEAKB9+/ZwdHSU9sXExGDYsGGYMGFCqRbW2mRjY4Nhw4aVWkF68OBBvPvuuwAACwsL9O/fv0BMeno6RowYgQ8++ECjwnrz5s0YP348Hj58iObNm8POzg7Jyck4evQo6tSpg4iICAwYMEDr16ILiYmJGDFiBP7880+tF9aayv/9qV+/PoKCgiCEwK1bt3Do0CG8+eabWLduHaysrErt/AMGDEDDhg1LrX+iCkcQkV7ZuHGjACCWLFlSpueNjY0V1atXF3v27JHacnJyRN++fYWxsbG4cuWKWvz3338vDA0NxeHDh6W2hQsXCgBi586dxZ5rzpw5AoDYt2+fWvvkyZOFu7u7MDc3F3/++afavnnz5gkAYvfu3f/1EjXy9OlTAUBMnz69VM+jDf379xe1atUSb7zxhmjXrl2hMffv3xcAxAcffPDK/n755RcBQPzvf/8Tz58/V9uXmpoqhg0bJnr06KGV3MuDCxcuCAAFvmvaoOn3qKjfn6ioKAFAfPzxx1rPjYiKxhFrokpCpVIhOjoat27dgpWVFVq0aAF7e3u1mBUrVsDDwwMtWrTApUuXcOXKFdSoUQOtW7eGkZFRsf1XrVoVJ0+eRM2aNaU2Y2Nj/O9//8OaNWvw119/oUGDBgBejFbPnj0b7du3R+vWraX4d999F9OnT8f333+PTp06FXmudu3aAQAOHDiA9u3bS+0HDhxAhw4dcPPmTRw4cAD9+vVT22dqaoqWLVuq3ZOTJ0/i5s2bsLKyQvPmzeHg4KB2rpUrV8Ld3R0tW7bEtWvXcO7cOdSrVw9NmjQBANy/fx9HjhyBqakp2rdvD0PDwh9dycvLQ3R0NBITE2FnZwd/f/8C9/9l6enpWLduHdq2bYvatWsDAB4+fIjNmzejQ4cOqFmzJg4fPoy7d+/Cx8cHfn5+xfb3b/nTGKZOnQpHR0e8++67SEhIkM5TUrdv38bHH3+M8PBwfPfd... (line truncated to 2000 chars)
4040:       "text/plain": [
4041:        "<Figure size 800x600 with 1 Axes>"
4042:       ]
4043:      },
4044:      "metadata": {},
4045:      "output_type": "display_data"
4046:     }
4047:    ],
4048:    "source": [
4049:     "plot_top_words(yelp_sample, 0, \"Top 20 Words in Genuine Reviews\")\n",
4050:     "\n",
4051:     "plot_top_words(yelp_sample, 1, \"Top 20 Words in AI Generated Reviews\")"
4052:    ]
4053:   },
4054:   {
4055:    "cell_type": "code",
4056:    "execution_count": 628,
4057:    "id": "ac76aa3f",
4058:    "metadata": {},
4059:    "outputs": [
4060:     {
4061:      "data": {
4062:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAA3IAAAIOCAYAAAD9QD/vAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAtDhJREFUeJzs3XdYVEf7N/AvdZGOUqQLKqAidkUjCgo2LFhjN/YYu9Ek2Dtq9JHYu7F3Y4kdBXvHLmABBASlygLC0vb9w5fzc6mLGnHl+7muvZ6cOXNm7jngc+3NzJmjJJVKpSAiIiIiIiKFoVzWARAREREREVHpMJEjIiIiIiJSMEzkiIiIiIiIFAwTOSIiIiIiIgXDRI6IiIiIiEjBMJEjIiIiIiJSMEzkiIiIiIiIFAwTOSIiIiIiIgXDRI6IiL6KVatWQV9fH8nJyWUdSpko7+Mvzw4fPgx9fX08evSorEMp0v3796Gvr48TJ06UdShEJCcmckRECuT8+fPQ19eX63P//v3/NJYdO3bI9GdgYICqVauibdu2OHLkSIH6GRkZSE5OhlQq/U/j+lb91+PP+3nUrl27yD7y6pw/f16uNmNiYjBjxgw0bdoUFhYWsLS0hLOzMwYPHgw/Pz/k5uZ+ySGUqaVLl0JfXx9paWlfvO3MzEwkJycjJyen2Hr5/00ZGhrCwcEBw4cPR1hY2BeP62PZ2dlITk5GVlbWf9oPEX05TOSIiBRIy5YtER4eLvPR0tKCjY1NgfLatWv/p7FIJBIkJydj8+bNCA8PR1hYGE6ePIlq1aqha9euWLlypUz9sWPHIikpCXp6ev9pXN+q/3r869atg7q6Oh4/flxkopb3M5Pny/qJEyfg4OCAgIAA/P7777h27Rpu3bqFhQsXIisrC23atMHff//9hUdRdr6FPzTk/zf15MkTLFu2DKdPn4azszNiY2P/s77r1auHpKQkeHp6/md9ENGXxUSOiEiBqKqqFph5U1JSgoqKSoFyFRWVrxKTlpaW0Ke9vT1WrVoFU1NTbN68WaaeSCQS4i2P/svxBwUF4dq1a/jf//6H6tWrY+PGjZ/V3tOnT9GzZ0+0atUKAQEB8PLygpWVFUxNTdGqVSvs3LkTJ06cgKam5hcaAX0s79+UiYkJPD09sWjRIsTGxmLbtm3/WZ95/x+ipqb2n/VBRF8WEzkiou/Q48eP0bt3b1hbWwtfvo8ePSpTZ8GCBdDX18f79+8xefJk2NjYwNraGiNHjkRCQsIn962kpASRSFQgkSzqGbGrV6+idevWqFy5MurXr4/9+/cX+kxRXrzp6emYOnUq7OzsUK1aNQDA/v37ZZZ4WlhYoH379jhz5kyhY05PT8dvv/0GW1tbVK9eHcuXLwfwYUZkypQpqFq1KqytrTF16tQCywcTEhIwadIk1K5dG6ampmjatCmWLFmCjIyMYu9LYePPi0cikWDmzJmoWrUqLC0tMXTo0FI9S7dx40YYGRmhV69e+Pnnn3HkyBHEx8fLfX1+8+bNQ2ZmJlasWFHkHwTat2+P3r17y5RFR0dj7NixcHBwgLGxMRo2bIg1a9bIzHKVdsylafNTfzfGjRuHBQsWAAAsLCwKXZ4sTxwAcP36dbi7u8v8Pn+umjVrAgDCw8NlyiUSCXx8fNCgQQOYmJjA3t4eU6ZMQUpKilDfwMAAS5YsKdBmYmIijI2NMX36dABFPyNXUh/Z2dmwsLDAjBkzZK6rVasW9PX1ERQUJJTlLQ2/evUqACA3NxfLly9H48aNYWZmhjp16mDMmDGIiYn5jLtFVH4wkSMi+s7cvXsXTZo0QXx8PA4fPoxLly6hQYMG8PLyklnumJ6ejuTkZIwfPx729va4ePEi1q9fj1OnTqF169YlJiaFkUgkWLZsGcLDwzFkyBCZc4UtXbt27RpatWoFAwMDnD17Frt378aFCxdw6NChAs8UfRyvtbU1zpw5g19++QUA0LVrV2FJ... (line truncated to 2000 chars)
4063:       "text/plain": [
4064:        "<Figure size 900x600 with 1 Axes>"
4065:       ]
4066:      },
4067:      "metadata": {},
4068:      "output_type": "display_data"
4069:     }
4070:    ],
4071:    "source": [
4072:     "vectorizer = CountVectorizer(\n",
4073:     "    stop_words=\"english\",\n",
4074:     "    ngram_range=(2,2),\n",
4075:     "    max_features=20\n",
4076:     ")\n",
4077:     "\n",
4078:     "X = vectorizer.fit_transform(amazon_df[amazon_df[\"label\"] == 1][\"review\"])\n",
4079:     "\n",
4080:     "counts = np.asarray(X.sum(axis=0)).flatten()\n",
4081:     "\n",
4082:     "bigrams = vectorizer.get_feature_names_out()\n",
4083:     "\n",
4084:     "pairs = sorted(zip(bigrams, counts), key=lambda x: x[1], reverse=True)\n",
4085:     "\n",
4086:     "bigrams, counts = zip(*pairs)\n",
4087:     "\n",
4088:     "plt.figure(figsize=(9,6))\n",
4089:     "plt.barh(bigrams, counts)\n",
4090:     "plt.title(\"Top Bigrams in AI Generated Reviews\")\n",
4091:     "plt.gca().invert_yaxis()\n",
4092:     "plt.show()"
4093:    ]
4094:   },
4095:   {
4096:    "cell_type": "code",
4097:    "execution_count": 629,
4098:    "id": "f37d5337",
4099:    "metadata": {},
4100:    "outputs": [
4101:     {
4102:      "data": {
4103:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAA1wAAAIOCAYAAACs1AyMAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAp0NJREFUeJzs3XdYVFfbLvB7hjL0IiIoIiAiiij2brBgQUFsiQ1jL7HEGpVEXzUaNRqNicYWC1Gx944FsRc0dmwICCogKDIUGdo+f3jYnyMDDMYRhft3XVzn3Ws/e61nb/A782StvUYiCIIAIiIiIiIi+uikxZ0AERERERFRScWCi4iIiIiISENYcBEREREREWkICy4iIiIiIiINYcFFRERERESkISy4iIiIiIiINIQFFxERERERkYaw4CIiIiIiItIQFlxERJSHp6cnvLy8ijuNYlPa7780Gzx4MGrVqlXcaRTol19+gZmZWXGnQURqYsFFRKQhEyZMgJmZWaE/NWrU0HguvXr1UhrTwsICrq6uGDhwIEJDQ/PEJycnIyUlReN5fa40ff+5v48pU6YUGGNtba12n5cvX8bgwYPh6uoKKysrODk5oVWrVvjpp5/w8OHDj5H2Z6NVq1bo0qWLRvpOTU2FXC4vNO79f1NWVlZo0KAB5s6di/T0dI3kluvNmzdISkrS6BhE9PGw4CIi0pBffvkFkZGR4s/evXuRlJSE0aNHK7VfvHhR47mkpKQgPT1dHPPBgwdYvXo1QkND0aBBA9y/f18p/ujRozh48KDG8/pcafL+Y2JisGvXLujq6mLt2rVQKBQq41JSUvD69Wu1+pw0aRKaNm0KXV1drFq1Cjdv3sSxY8cwdOhQHD16FM7Oznj58uVHvIvi9Tn8B4H3/01dvnwZvXv3xrRp09CrVy+Njj1t2jQkJiZqdAwi+ni0izsBIqKSSl9fH/r6+uKxkZERAEBPT6/YlgO9O27ZsmXx559/onHjxti6dStmzpwpnsvNtbTS5P2vX78e2tra2LFjB1q2bIndu3ejd+/eH9zf77//jkWLFmHt2rUYNGiQ0jkHBwf07NkTfn5+/zVtykfuvykzMzNMmDABFy9exM6dO/Ho0SM4OTlpZEw9PT3o6elppG8i+vg4w0VEVMy2bdsGd3d3WFtbw97eHr6+vnmWgDVt2hS9evXC48eP4ePjgwoVKqBmzZpYsmQJBEH44LFzP7RpaWkptef3DtPSpUtRq1YtlC9fHp06dcK9e/dUvvOSm29ERAS+/vprVKxYEd9//z0AoH///kpLG52cnDBo0CA8efJEZR/h4eHo0qULKlSogCZNmuDcuXMAgLCwMHTt2hU2NjZwc3PD3r178+R79epVdO/eHVWqVEGlSpXQoUMHHDp0qNDnour+c/N5+vQpvv76a1SoUAEuLi74448/Cu0vlyAIWLduHb755hu4u7ujRYsWWLNmjdrXvy89PR2zZ89GgwYN8hRbubS0tLBgwQJYWFgotZ87dw5dunRBpUqVUL58eXh6euL8+fNKMUW956L0+aF/G46Ojrhx4wZOnz6d77JcdfIAgOXLl8PNzU3p7/m/cnFxAQBERkYqtUdGRmLYsGFwcnJCuXLl0LhxY6xfv14pFzMzM9y9ezdPn1u3boWZmZk4G57fO1yFjXHy5EmYmZnh0qVLYtv169dhZmaGunXrKvU1YcIEVK5cWfy/LzExMRg1ahRq1KiBChUqoFmzZvjzzz+RmZlZtAdEVBoJRET0SYSEhAgAhNmzZ4ttc+fOFSQSiTBt2jQhLCxMuHz5stC8eXPBxMREuHPnjhhXo0YN4auvvhI8PDyEoKAgISIiQli8eLGgra0tTJ48udCxO3XqJMhkMqW2mJgYwdvbWzA0NBTu37+vdK5Zs2aCu7u7Utu0adMELS0tYcGCBUJERIRw7tw5oV27doKHh4dgZ2enFJubb9u2bYWTJ08KDx48EPz9/QVB... (line truncated to 2000 chars)
4104:       "text/plain": [
4105:        "<Figure size 900x600 with 1 Axes>"
4106:       ]
4107:      },
4108:      "metadata": {},
4109:      "output_type": "display_data"
4110:     }
4111:    ],
4112:    "source": [
4113:     "vectorizer = CountVectorizer(\n",
4114:     "    stop_words=\"english\",\n",
4115:     "    ngram_range=(2,2),\n",
4116:     "    max_features=20\n",
4117:     ")\n",
4118:     "\n",
4119:     "X = vectorizer.fit_transform(yelp_sample[yelp_sample[\"label\"] == 1][\"review\"])\n",
4120:     "\n",
4121:     "counts = np.asarray(X.sum(axis=0)).flatten()\n",
4122:     "\n",
4123:     "bigrams = vectorizer.get_feature_names_out()\n",
4124:     "\n",
4125:     "pairs = sorted(zip(bigrams, counts), key=lambda x: x[1], reverse=True)\n",
4126:     "\n",
4127:     "bigrams, counts = zip(*pairs)\n",
4128:     "\n",
4129:     "plt.figure(figsize=(9,6))\n",
4130:     "plt.barh(bigrams, counts)\n",
4131:     "plt.title(\"Top Bigrams in AI Generated Reviews\")\n",
4132:     "plt.gca().invert_yaxis()\n",
4133:     "plt.show()"
4134:    ]
4135:   },
4136:   {
4137:    "cell_type": "code",
4138:    "execution_count": 630,
4139:    "id": "a728bb12",
4140:    "metadata": {},
4141:    "outputs": [
4142:     {
4143:      "data": {
4144:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArMAAAJOCAYAAACk64/cAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAi+JJREFUeJzs3XdYFFfbBvB7FxAsNBVEELGgIqixYxdErNiNYI0t9p7E2GsMscYeTew91thrFHvvXUQRFOxSlbZ7vj98mS8rxUUXdhbu33XN9b5z5syZZzYqD8+eOaMQQggQERERERkgpb4DICIiIiL6UkxmiYiIiMhgMZklIiIiIoPFZJaIiIiIDBaTWSIiIiIyWExmiYiIiMhgMZklIiIiIoPFZJaIiIiIDBaTWSIiIiIyWExmiYhSMWrUKBgbGxvMuIaOnwsRfSkms0SUJdRqNTZs2IAmTZrA1tYWpqamKFq0KBo0aIBly5YhNjZW3yHqzLBhw2BmZqbvMFL47bffoFAooFAocP78+VT7VKxYEQqFAs7Ozl90DbneOxFlX0xmiSjTxcXFoXnz5ujTpw88PT1x/vx5REdH49SpU2jatClGjBiBBQsW6DvMLPHbb78hKSlJrzHkzZsXq1atStF+9epVXL9+HXnz5s3ymOTwuRCRYWIyS0SZbujQoTh06BD27t2Ln3/+GcWLF0euXLlQtGhR/PTTT7h8+TKKFCmi7zBzjLZt22LTpk2Ii4vTaF+5ciWcnZ1RsWJF/QRGRPQFmMwSUaZ6+vQpli9fjnbt2qF+/fqp9ilVqhS6dOki7atUKkyfPh0uLi4wNTVFwYIF4evri4cPH2qcZ2VlhX79+uHs2bOoXbs2cufOjUmTJuHUqVNQKBTYs2cP/vjjDzg7O8PIyAiXLl0CANy+fRvffvstbGxsYGpqirJly2L+/PmfvZe5c+dKX9MrFApYWFigfv362L9/v9SndevWmDdvHuLj4zX6BgcHA0h7bujRo0fh6ekJc3Nz5MmTB+7u7ti+fbtGn379+sHKygoxMTHo2bMnrKysYGVlha5duyIqKuqz8Sfr1q0boqKisHPnTqktISEBGzZsQPfu3TPt3pPjj4iIQPfu3ZE/f36ULVs21c/lzZs3KFq0KKpUqaKRdD9//hz29vaoWbMmEhMTtb5nIsq+mMwSUaY6cuQIVCoVmjZtqvU5PXr0wKRJkzBy5Ei8ePECR48eRXBwMNzd3fH48WONvo8fP4a/vz/++usvBAYGonLlytKxFStW4NmzZzh58iQCAgKQO3duXLhwAdWrV0diYiJOnDiB169fY+rUqRg/fjxGjRqVblzDhg2DEAJCCKhUKty8eROVKlVCq1atcOXKFQDAP//8g6FDh8LU1FTqK4RAsWLF0hx39+7d8Pb2hpOTE27duoWgoCDUr18f7dq1w9KlS1P0Hzx4MNq3b4/Q0FD8/fff2LlzJ0aOHKn151ukSBE0bNhQY6rBrl278O7dO3Tr1i3T771fv35o3749goKC0oy7QIEC2LJlC27evInBgwcD+PhLjp+fHxITE7F582aYmJhofc9ElI0JIqJMNGnSJAFAHDlyRKv+V65cEQDEhAkTNNqfPn0qTE1NxXfffSe1WVpairx584o3b95o9D158qQAILy9vVOMX61aNVGqVCkRHx+v0T5r1ixhbGwswsLChBBC/Pzzz8LIyEirmIsVKyYGDRok7Q8dOlSYmpqm2je1cUuXLi1cXFyESqXSaPfy8hJWVlbi/fv3Qggh+vbtKwCIzZs3a/QbPHiwyJUrl0hMTEw3Tn9/fwFA3L17V2zYsEEYGRmJZ8+eCSGEaNasmfR51a5dW5QsWVKLO8/YvSfHv3r16hTH0vq858+fLwCIlStXipEjRwqlUikOHjyoVWxElDOwMktEsvLvv/8C+Div878cHBxQo0YN6XiyOnXqIH/+/KmO1bJlS439Fy9e4OLFi2jVqhVy... (line truncated to 2000 chars)
4145:       "text/plain": [
4146:        "<Figure size 800x600 with 2 Axes>"
4147:       ]
4148:      },
4149:      "metadata": {},
4150:      "output_type": "display_data"
4151:     }
4152:    ],
4153:    "source": [
4154:     "feature_cols = [\n",
4155:     "    \"text_length\",\n",
4156:     "    \"word_count\",\n",
4157:     "    \"sentence_count\",\n",
4158:     "    \"avg_word_len\",\n",
4159:     "    \"vocab_richness\",\n",
4160:     "    \"label\"\n",
4161:     "]\n",
4162:     "\n",
4163:     "corr = amazon_df[feature_cols].corr()\n",
4164:     "\n",
4165:     "plt.figure(figsize=(8,6))\n",
4166:     "plt.imshow(corr)\n",
4167:     "\n",
4168:     "plt.colorbar()\n",
4169:     "\n",
4170:     "plt.xticks(range(len(feature_cols)), feature_cols, rotation=45)\n",
4171:     "\n",
4172:     "plt.yticks(range(len(feature_cols)), feature_cols)\n",
4173:     "\n",
4174:     "plt.title(\"Correlation Matrix\")\n",
4175:     "\n",
4176:     "plt.tight_layout()\n",
4177:     "plt.show()"
4178:    ]
4179:   },
4180:   {
4181:    "cell_type": "code",
4182:    "execution_count": 631,
4183:    "id": "73665682",
4184:    "metadata": {},
4185:    "outputs": [
4186:     {
4187:      "data": {
4188:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArMAAAJOCAYAAACk64/cAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAi95JREFUeJzs3XdYFFfbBvB7KYIiRQFFqiIiYokdFY2gYu8Ne9QYNZZYkhh7T4gxGnuJLXaNLRq7RrHE3k1EBBRFwIJKVdru+f7wZb6sFBdd2Fm4f9c115s5c+bMM/uKPD575oxCCCFARERERKSHDHQdABERERHRh2IyS0RERER6i8ksEREREektJrNEREREpLeYzBIRERGR3mIyS0RERER6i8ksEREREektJrNEREREpLeYzBIRERGR3mIyS0SUhfHjx8PIyEhvxtV3/FyI6EMxmSWifKFSqbBlyxa0bNkSpUqVgomJCZydndGkSROsXr0aSUlJug5Ra0aPHg1TU1Ndh5HJjz/+CIVCAYVCgYsXL2bZp3r16lAoFHBzc/uga8j13omo4GIyS0R5Ljk5GW3atMHgwYPh6+uLixcvIiEhAWfPnkWrVq0wduxYLF68WNdh5osff/wR6enpOo3BzMwMv/32W6b269ev4+bNmzAzM8v3mOTwuRCRfmIyS0R5btSoUTh69CgOHDiA7777DuXKlUORIkXg7OyMb7/9FlevXoWjo6Ouwyw0OnfujG3btiE5OVmtfd26dXBzc0P16tV1ExgR0QdgMktEeerx48dYs2YNunTpgsaNG2fZp0KFCujTp4+0r1QqMWfOHHh4eMDExAQ2Njbw9/dHaGio2nlWVlYYOnQozp8/D29vbxQtWhTTp0/H2bNnoVAosH//fixfvhxubm4wNDTElStXAAD//vsvunXrBltbW5iYmKBSpUpYtGjRe+9lwYIF0tf0CoUCFhYWaNy4MQ4dOiT16dixIxYuXIiUlBS1vuHh4QCynxt64sQJ+Pr6wtzcHMWKFYOXlxd2796t1mfo0KGwsrJCYmIiBg4cCCsrK1hZWaFv376Ij49/b/wZ+vXrh/j4eOzdu1dqS01NxZYtW9C/f/88u/eM+GNjY9G/f3+ULFkSlSpVyvJzefHiBZydnVGrVi21pPvJkyewt7dH/fr1kZaWpvE9E1HBxWSWiPLU8ePHoVQq0apVK43PGTBgAKZPn45x48bh6dOnOHHiBMLDw+Hl5YUHDx6o9X3w4AECAgKwatUqhISEoGbNmtKxtWvXIjIyEmfOnEFgYCCKFi2KS5cuoW7dukhLS8Pp06cRExODWbNmYcqUKRg/fnyOcY0ePRpCCAghoFQqcfv2bdSoUQMdOnTAtWvXAAB//PEHRo0aBRMTE6mvEAJly5bNdtw///wTfn5+cHFxwT///IOwsDA0btwYXbp0wcqVKzP1HzlyJLp27YqIiAhs374de/fuxbhx4zT+fB0dHdGsWTO1qQb79u3Dq1ev0K9fvzy/96FDh6Jr164ICwvLNm5ra2vs2LEDt2/fxsiRIwG8/UdOjx49kJaWht9//x3GxsYa3zMRFWCCiCgPTZ8+XQAQx48f16j/tWvXBAAxdepUtfbHjx8LExMT8dlnn0ltlpaWwszMTLx48UKt75kzZwQA4efnl2n8OnXqiAoVKoiUlBS19p9//lkYGRmJqKgoIYQQ3333nTA0NNQo5rJly4oRI0ZI+6NGjRImJiZZ9s1qXHd3d+Hh4SGUSqVae9OmTYWVlZV4/fq1EEKIIUOGCADi999/V+s3cuRIUaRIEZGWlpZjnAEBAQKACAoKElu2bBGGhoYiMjJSCCFE69atpc/L29tblC9fXoM7z929Z8S/fv36TMey+7wXLVokAIh169aJcePGCQMDA3HkyBGNYiOiwoGVWSKSlb/++gvA23md/+Xg4IB69epJxzM0bNgQJUuWzHKs9u3bq+0/ffoUly9fRocO... (line truncated to 2000 chars)
4189:       "text/plain": [
4190:        "<Figure size 800x600 with 2 Axes>"
4191:       ]
4192:      },
4193:      "metadata": {},
4194:      "output_type": "display_data"
4195:     }
4196:    ],
4197:    "source": [
4198:     "feature_cols = [\n",
4199:     "    \"text_length\",\n",
4200:     "    \"word_count\",\n",
4201:     "    \"sentence_count\",\n",
4202:     "    \"avg_word_len\",\n",
4203:     "    \"vocab_richness\",\n",
4204:     "    \"label\"\n",
4205:     "]\n",
4206:     "\n",
4207:     "corr = yelp_sample[feature_cols].corr()\n",
4208:     "\n",
4209:     "plt.figure(figsize=(8,6))\n",
4210:     "plt.imshow(corr)\n",
4211:     "\n",
4212:     "plt.colorbar()\n",
4213:     "\n",
4214:     "plt.xticks(range(len(feature_cols)), feature_cols, rotation=45)\n",
4215:     "\n",
4216:     "plt.yticks(range(len(feature_cols)), feature_cols)\n",
4217:     "\n",
4218:     "plt.title(\"Correlation Matrix\")\n",
4219:     "\n",
4220:     "plt.tight_layout()\n",
4221:     "plt.show()"
4222:    ]
4223:   },
4224:   {
4225:    "cell_type": "code",
4226:    "execution_count": 632,
4227:    "id": "ad75625e",
4228:    "metadata": {},
4229:    "outputs": [
4230:     {
4231:      "data": {
4232:       "text/html": [
4233:        "<div>\n",
4234:        "<style scoped>\n",
4235:        "    .dataframe tbody tr th:only-of-type {\n",
4236:        "        vertical-align: middle;\n",
4237:        "    }\n",
4238:        "\n",
4239:        "    .dataframe tbody tr th {\n",
4240:        "        vertical-align: top;\n",
4241:        "    }\n",
4242:        "\n",
4243:        "    .dataframe thead tr th {\n",
4244:        "        text-align: left;\n",
4245:        "    }\n",
4246:        "\n",
4247:        "    .dataframe thead tr:last-of-type th {\n",
4248:        "        text-align: right;\n",
4249:        "    }\n",
4250:        "</style>\n",
4251:        "<table border=\"1\" class=\"dataframe\">\n",
4252:        "  <thead>\n",
4253:        "    <tr>\n",
4254:        "      <th></th>\n",
4255:        "      <th colspan=\"8\" halign=\"left\">text_length</th>\n",
4256:        "      <th colspan=\"8\" halign=\"left\">word_count</th>\n",
4257:        "      <th colspan=\"8\" halign=\"left\">sentence_count</th>\n",
4258:        "      <th colspan=\"8\" halign=\"left\">avg_word_len</th>\n",
4259:        "      <th colspan=\"8\" halign=\"left\">vocab_richness</th>\n",
4260:        "    </tr>\n",
4261:        "    <tr>\n",
4262:        "      <th></th>\n",
4263:        "      <th>count</th>\n",
4264:        "      <th>mean</th>\n",
4265:        "      <th>std</th>\n",
4266:        "      <th>min</th>\n",
4267:        "      <th>25%</th>\n",
4268:        "      <th>50%</th>\n",
4269:        "      <th>75%</th>\n",
4270:        "      <th>max</th>\n",
4271:        "      <th>count</th>\n",
4272:        "      <th>mean</th>\n",
4273:        "      <th>std</th>\n",
4274:        "      <th>min</th>\n",
4275:        "      <th>25%</th>\n",
4276:        "      <th>50%</th>\n",
4277:        "      <th>75%</th>\n",
4278:        "      <th>max</th>\n",
4279:        "      <th>count</th>\n",
4280:        "      <th>mean</th>\n",
4281:        "      <th>std</th>\n",
4282:        "      <th>min</th>\n",
4283:        "      <th>25%</th>\n",
4284:        "      <th>50%</th>\n",
4285:        "      <th>75%</th>\n",
4286:        "      <th>max</th>\n",
4287:        "      <th>count</th>\n",
4288:        "      <th>mean</th>\n",
4289:        "      <th>std</th>\n",
4290:        "      <th>min</th>\n",
4291:        "      <th>25%</th>\n",
4292:        "      <th>50%</th>\n",
4293:        "      <th>75%</th>\n",
4294:        "      <th>max</th>\n",
4295:        "      <th>count</th>\n",
4296:        "      <th>mean</th>\n",
4297:        "      <th>std</th>\n",
4298:        "      <th>min</th>\n",
4299:        "      <th>25%</th>\n",
4300:        "      <th>50%</th>\n",
4301:        "      <th>75%</th>\n",
4302:        "      <th>max</th>\n",
4303:        "    </tr>\n",
4304:        "    <tr>\n",
4305:        "      <th>label</th>\n",
4306:        "      <th></th>\n",
4307:        "      <th></th>\n",
4308:        "      <th></th>\n",
4309:        "      <th></th>\n",
4310:        "      <th></th>\n",
4311:        "      <th></th>\n",
4312:        "      <th></th>\n",
4313:        "      <th></th>\n",
4314:        "      <th></th>\n",
4315:        "      <th></th>\n",
4316:        "      <th></th>\n",
4317:        "      <th></th>\n",
4318:        "      <th></th>\n",
4319:        "      <th></th>\n",
4320:        "      <th></th>\n",
4321:        "      <th></th>\n",
4322:        "      <th></th>\n",
4323:        "      <th></th>\n",
4324:        "      <th></th>\n",
4325:        "      <th></th>\n",
4326:        "      <th></th>\n",
4327:        "      <th></th>\n",
4328:        "      <th></th>\n",
4329:        "      <th></th>\n",
4330:        "      <th></th>\n",
4331:        "      <th></th>\n",
4332:        "      <th></th>\n",
4333:        "      <th></th>\n",
4334:        "      <th></th>\n",
4335:        "      <th></th>\n",
4336:        "      <th></th>\n",
4337:        "      <th></th>\n",
4338:        "      <th></th>\n",
4339:        "      <th></th>\n",
4340:        "      <th></th>\n",
4341:        "      <th></th>\n",
4342:        "      <th></th>\n",
4343:        "      <th></th>\n",
4344:        "      <th></th>\n",
4345:        "      <th></th>\n",
4346:        "    </tr>\n",
4347:        "  </thead>\n",
4348:        "  <tbody>\n",
4349:        "    <tr>\n",
4350:        "      <th>0</th>\n",
4351:        "      <td>20215.0</td>\n",
4352:        "      <td>383.558348</td>\n",
4353:        "      <td>402.202223</td>\n",
4354:        "      <td>24.0</td>\n",
4355:        "      <td>117.0</td>\n",
4356:        "      <td>217.0</td>\n",
4357:        "      <td>484.0</td>\n",
4358:        "      <td>2095.0</td>\n",
4359:        "      <td>20215.0</td>\n",
4360:        "      <td>75.199159</td>\n",
4361:        "      <td>77.811015</td>\n",
4362:        "      <td>5.0</td>\n",
4363:        "      <td>23.0</td>\n",
4364:        "      <td>43.0</td>\n",
4365:        "      <td>95.0</td>\n",
4366:        "      <td>381.0</td>\n",
4367:        "      <td>20215.0</td>\n",
4368:        "      <td>1.0</td>\n",
4369:        "      <td>0.0</td>\n",
4370:        "      <td>1.0</td>\n",
4371:        "      <td>1.0</td>\n",
4372:        "      <td>1.0</td>\n",
4373:        "      <td>1.0</td>\n",
4374:        "      <td>1.0</td>\n",
4375:        "      <td>20215.0</td>\n",
4376:        "      <td>4.109831</td>\n",
4377:        "      <td>0.436404</td>\n",
4378:        "      <td>2.545455</td>\n",
4379:        "      <td>3.827659</td>\n",
4380:        "      <td>4.074074</td>\n",
4381:        "      <td>4.352941</td>\n",
4382:        "      <td>7.300000</td>\n",
4383:        "      <td>20215.0</td>\n",
4384:        "      <td>0.803361</td>\n",
4385:        "      <td>0.133560</td>\n",
4386:        "      <td>0.317073</td>\n",
4387:        "      <td>0.704545</td>\n",
4388:        "      <td>0.815789</td>\n",
4389:        "      <td>0.909091</td>\n",
4390:        "      <td>1.0</td>\n",
4391:        "    </tr>\n",
4392:        "    <tr>\n",
4393:        "      <th>1</th>\n",
4394:        "      <td>20192.0</td>\n",
4395:        "      <td>296.262827</td>\n",
4396:        "      <td>298.076633</td>\n",
4397:        "      <td>37.0</td>\n",
4398:        "      <td>93.0</td>\n",
4399:        "      <td>169.0</td>\n",
4400:        "      <td>370.0</td>\n",
4401:        "      <td>1665.0</td>\n",
4402:        "      <td>20192.0</td>\n",
4403:        "      <td>63.140055</td>\n",
4404:        "      <td>63.753927</td>\n",
4405:        "      <td>7.0</td>\n",
4406:        "      <td>19.0</td>\n",
4407:        "      <td>36.0</td>\n",
4408:        "      <td>79.0</td>\n",
4409:        "      <td>322.0</td>\n",
4410:        "      <td>20192.0</td>\n",
4411:        "      <td>1.0</td>\n",
4412:        "      <td>0.0</td>\n",
4413:        "      <td>1.0</td>\n",
4414:        "      <td>1.0</td>\n",
4415:        "      <td>1.0</td>\n",
4416:        "      <td>1.0</td>\n",
4417:        "      <td>1.0</td>\n",
4418:        "      <td>20192.0</td>\n",
4419:        "      <td>3.765257</td>\n",
4420:        "      <td>0.419527</td>\n",
4421:        "      <td>1.666667</td>\n",
4422:        "      <td>3.488372</td>\n",
4423:        "      <td>3.714286</td>\n",
4424:        "      <td>3.977549</td>\n",
4425:        "      <td>7.636364</td>\n",
4426:        "      <td>20192.0</td>\n",
4427:        "      <td>0.721480</td>\n",
4428:        "      <td>0.182635</td>\n",
4429:        "      <td>0.029412</td>\n",
4430:        "      <td>0.593750</td>\n",
4431:        "      <td>0.750000</td>\n",
4432:        "      <td>0.869565</td>\n",
4433:        "      <td>1.0</td>\n",
4434:        "    </tr>\n",
4435:        "  </tbody>\n",
4436:        "</table>\n",
4437:        "</div>"
4438:       ],
4439:       "text/plain": [
4440:        "      text_length                                                             \\\n",
4441:        "            count        mean         std   min    25%    50%    75%     max   \n",
4442:        "label                                                                          \n",
4443:        "0         20215.0  383.558348  402.202223  24.0  117.0  217.0  484.0  2095.0   \n",
4444:        "1         20192.0  296.262827  298.076633  37.0   93.0  169.0  370.0  1665.0   \n",
4445:        "\n",
4446:        "      word_count                                                      \\\n",
4447:        "           count       mean        std  min   25%   50%   75%    max   \n",
4448:        "label                                                                  \n",
4449:        "0        20215.0  75.199159  77.811015  5.0  23.0  43.0  95.0  381.0   \n",
4450:        "1        20192.0  63.140055  63.753927  7.0  19.0  36.0  79.0  322.0   \n",
4451:        "\n",
4452:        "      sentence_count                                    avg_word_len  \\\n",
4453:        "               count mean  std  min  25%  50%  75%  max        count   \n",
4454:        "label                                                                  \n",
4455:        "0            20215.0  1.0  0.0  1.0  1.0  1.0  1.0  1.0      20215.0   \n",
4456:        "1            20192.0  1.0  0.0  1.0  1.0  1.0  1.0  1.0      20192.0   \n",
4457:        "\n",
4458:        "                                                                             \\\n",
4459:        "           mean       std       min       25%       50%       75%       max   \n",
4460:        "label                                                                         \n",
4461:        "0      4.109831  0.436404  2.545455  3.827659  4.074074  4.352941  7.300000   \n",
4462:        "1      3.765257  0.419527  1.666667  3.488372  3.714286  3.977549  7.636364   \n",
4463:        "\n",
4464:        "      vocab_richness                                                    \\\n",
4465:        "               count      mean       std       min       25%       50%   \n",
4466:        "label                                                                    \n",
4467:        "0            20215.0  0.803361  0.133560  0.317073  0.704545  0.815789   \n",
4468:        "1            20192.0  0.721480  0.182635  0.029412  0.593750  0.750000   \n",
4469:        "\n",
4470:        "                      \n",
4471:        "            75%  max  \n",
4472:        "label                 \n",
4473:        "0      0.909091  1.0  \n",
4474:        "1      0.869565  1.0  "
4475:       ]
4476:      },
4477:      "execution_count": 632,
4478:      "metadata": {},
4479:      "output_type": "execute_result"
4480:     }
4481:    ],
4482:    "source": [
4483:     "summary = amazon_df.groupby(\"label\")[\n",
4484:     "    [\n",
4485:     "        \"text_length\",\n",
4486:     "        \"word_count\",\n",
4487:     "        \"sentence_count\",\n",
4488:     "        \"avg_word_len\",\n",
4489:     "        \"vocab_richness\"\n",
4490:     "    ]\n",
4491:     "].describe()\n",
4492:     "\n",
4493:     "summary"
4494:    ]
4495:   },
4496:   {
4497:    "cell_type": "code",
4498:    "execution_count": 638,
4499:    "id": "10f520a6",
4500:    "metadata": {},
4501:    "outputs": [
4502:     {
4503:      "data": {
4504:       "text/html": [
4505:        "<div>\n",
4506:        "<style scoped>\n",
4507:        "    .dataframe tbody tr th:only-of-type {\n",
4508:        "        vertical-align: middle;\n",
4509:        "    }\n",
4510:        "\n",
4511:        "    .dataframe tbody tr th {\n",
4512:        "        vertical-align: top;\n",
4513:        "    }\n",
4514:        "\n",
4515:        "    .dataframe thead th {\n",
4516:        "        text-align: right;\n",
4517:        "    }\n",
4518:        "</style>\n",
4519:        "<table border=\"1\" class=\"dataframe\">\n",
4520:        "  <thead>\n",
4521:        "    <tr style=\"text-align: right;\">\n",
4522:        "      <th></th>\n",
4523:        "      <th>count</th>\n",
4524:        "      <th>mean</th>\n",
4525:        "      <th>std</th>\n",
4526:        "      <th>min</th>\n",
4527:        "      <th>25%</th>\n",
4528:        "      <th>50%</th>\n",
4529:        "      <th>75%</th>\n",
4530:        "      <th>max</th>\n",
4531:        "    </tr>\n",
4532:        "    <tr>\n",
4533:        "      <th>label</th>\n",
4534:        "      <th></th>\n",
4535:        "      <th></th>\n",
4536:        "      <th></th>\n",
4537:        "      <th></th>\n",
4538:        "      <th></th>\n",
4539:        "      <th></th>\n",
4540:        "      <th></th>\n",
4541:        "      <th></th>\n",
4542:        "    </tr>\n",
4543:        "  </thead>\n",
4544:        "  <tbody>\n",
4545:        "    <tr>\n",
4546:        "      <th>0</th>\n",
4547:        "      <td>20215.0</td>\n",
4548:        "      <td>0.803361</td>\n",
4549:        "      <td>0.133560</td>\n",
4550:        "      <td>0.317073</td>\n",
4551:        "      <td>0.704545</td>\n",
4552:        "      <td>0.815789</td>\n",
4553:        "      <td>0.909091</td>\n",
4554:        "      <td>1.0</td>\n",
4555:        "    </tr>\n",
4556:        "    <tr>\n",
4557:        "      <th>1</th>\n",
4558:        "      <td>20192.0</td>\n",
4559:        "      <td>0.721480</td>\n",
4560:        "      <td>0.182635</td>\n",
4561:        "      <td>0.029412</td>\n",
4562:        "      <td>0.593750</td>\n",
4563:        "      <td>0.750000</td>\n",
4564:        "      <td>0.869565</td>\n",
4565:        "      <td>1.0</td>\n",
4566:        "    </tr>\n",
4567:        "  </tbody>\n",
4568:        "</table>\n",
4569:        "</div>"
4570:       ],
4571:       "text/plain": [
4572:        "         count      mean       std       min       25%       50%       75%  \\\n",
4573:        "label                                                                        \n",
4574:        "0      20215.0  0.803361  0.133560  0.317073  0.704545  0.815789  0.909091   \n",
4575:        "1      20192.0  0.721480  0.182635  0.029412  0.593750  0.750000  0.869565   \n",
4576:        "\n",
4577:        "       max  \n",
4578:        "label       \n",
4579:        "0      1.0  \n",
4580:        "1      1.0  "
4581:       ]
4582:      },
4583:      "execution_count": 638,
4584:      "metadata": {},
4585:      "output_type": "execute_result"
4586:     }
4587:    ],
4588:    "source": [
4589:     "amazon_df.groupby(\"label\")[\"vocab_richness\"].describe()"
4590:    ]
4591:   },
4592:   {
4593:    "cell_type": "code",
4594:    "execution_count": 635,
4595:    "id": "c09ef612",
4596:    "metadata": {},
4597:    "outputs": [
4598:     {
4599:      "data": {
4600:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAhsAAAHCCAYAAABG/gvHAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATd1JREFUeJzt3XlYVGX/BvB72AdBQFDcUExEEDEF9yVJxSVxKdfSNAPN0kpTTEstc8HUUtPXNHHNXXN5TXMrzSX3FVRyRRRRFNmUHZ7fH/44ryMDzAznMAL357q4imee85zvbIfbszxHJYQQICIiIlKIibELICIiotKNYYOIiIgUxbBBREREimLYICIiIkUxbBAREZGiGDaIiIhIUQwbREREpCiGDSIiIlIUw8YrJCUlBaGhobhy5Yqs42ZlZSE0NBSXLl2SddziZOhzUOo1JXmVhs8olXy//vorjh07ZuwyCrRjxw7s3bvX2GXoTVVWZhBNSkrCpk2b4OHhgdatW+fb78CBA7hz5w4GDRoEc3PzYqwQuHfvHlxcXLBgwQKMHDlStnGfPn0KW1tbhISEYPz48bKNW1TLly9HTk4OAEClUqFcuXLw9PTE66+/nqevoc9Bqde0JLl58ybCwsKQnJyMSpUqoUaNGvDw8IBKpTJ2aZJX9TOqhI0bNyI5ORnvvPMOKlSooLXP8uXLUaNGDXTo0EHncUvC+1xU6enp+PXXX9GsWTN4e3vLPr69vT369++PxYsXF9hPn22X3Bo3bgwnJyfs2bNH8XXJyczYBRSX3A2ZEAI3b97U+gVMT09Hv379ULduXQQGBhqhyrJl2LBhqF69urRBjY6OxoEDB+Dj44Pt27ejSpUqUl9zc3MEBgYWy5e5tDh8+DBGjx6Na9euoWXLlnB2dsajR49w5MgRODs7Y9SoUfj000+NXSaAsvP+Xrt2Df379wcAxMfHIzg4WGu/YcOGISAgQKewUZLe56JKTk7G0KFDMXv2bEXChq702XbJrWfPnrCxsVFsfMWIMmT69OkCgDhw4IDWx9etWycAiOXLlxdzZc/dvXtXABALFiyQddzk5GQBQISEhMg6blGZmpqKHj16aLQdOnRIqFQq0atXL1nWodRr+qrbtm2bMDU1FYMHDxYJCQkajyUnJ4tx48aJJk2aGKm6sis4OFiUL19edOrUSbi7u+fbT9t3Q5uy9j4/evRIABCzZ89WZHw7Ozvx0UcfFdqvOLZdpU2Z2bMBAEOGDME333yDZcuWoX379nkeDw0NRfny5dG3b1+pLTU1FUePHkVMTAwqVqyINm3aaE2VQgicOXMG169fh729PZo3b66xi3TVqlXIzMwE8PxfcdWqVUPr1q1hZWWVb71Hjx5FZGQk6tatiyZNmmg89ujRI+zYsQP+/v6oWbOmxmOrVq2Cu7s7WrRoUeDroUtNKSkpWLduHVq2bIl69erh5MmTiIiIQPPmzXH06FF4e3ujadOmecbevn07hBB4++23C6zhZW3btoWHh0eeY5JZWVlYuXIlmjZtigYNGmg8Vthr/6ITJ07gxo0bqF27dp7X5+XnWlDfXDk5OTh16hRu3LgBtVqN1q1bw9nZOU+/06dP4+bNm7CxsUGjRo1QrVo1vfscPHgQN2/exIABA6BWq7XWAwCJiYkYMmQImjZtiuXLl8PERPPULBsbG3z//fc4c+aM3s9Hn9dIn8+otvdXyfcjV1paGtasWYMGDRpo/Rzv2LEDOTk5Gp9jXd5LbTIzM7Fq1SoMGjQIPXr0gL+/Pw4fPow33nhDp+Vf9qq8z4aOmbstadu2LVxdXQvdHj1+/Bhr1qwBAJw6dQqhoaEAkOfQuK6fgSdPnuDgwYPIycmBn58fKlasqNPrnp/8tl25rl27hvPnzyM7Oxs+Pj7w8PCQHvvtt99gZmaGHj165Fnu1KlTCAsLw/vvvw8LCwvs2LEDVlZW6NSpk17r+PvvvxETEyPtWQOA... (line truncated to 2000 chars)
4601:       "text/plain": [
4602:        "<Figure size 600x500 with 1 Axes>"
4603:       ]
4604:      },
4605:      "metadata": {},
4606:      "output_type": "display_data"
4607:     }
4608:    ],
4609:    "source": [
4610:     "plt.figure(figsize=(6,5))\n",
4611:     "\n",
4612:     "plt.boxplot(\n",
4613:     "    [\n",
4614:     "        amazon_df[amazon_df[\"label\"] == 0][\"vocab_richness\"],\n",
4615:     "        amazon_df[amazon_df[\"label\"] == 1][\"vocab_richness\"]\n",
4616:     "    ],\n",
4617:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
4618:     ")\n",
4619:     "\n",
4620:     "plt.title(\"Vocabulary Richness: Genuine vs AI Generated Reviews\")\n",
4621:     "plt.ylabel(\"Vocabulary Richness\")\n",
4622:     "\n",
4623:     "plt.show()"
4624:    ]
4625:   },
4626:   {
4627:    "cell_type": "code",
4628:    "execution_count": 636,
4629:    "id": "1eaf3a70",
4630:    "metadata": {},
4631:    "outputs": [
4632:     {
4633:      "data": {
4634:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUUxJREFUeJzt3Xd0FdX+/vEnjYQE0gglhBZqIkiRpqCg0gJIR0EQUBGxAl7vRVAU9esVQRQRC/cKKqKCSBMURUQQgtIEpfcWSgiQQAKE1P37g1/O5ZDCOXBSyLxfa2WtnD17Zj5z5oQ87OyZcTPGGAEAAAAW4l7YBQAAAAAFjRAMAAAAyyEEAwAAwHIIwQAAALAcQjAAAAAshxAMAAAAyyEEAwAAwHIIwQAAALAcQjBQjJ09e1YRERH64osvCm1/R44cUUREhObOnVsgNeRWR1GUnp6ud955R/fcc48iIyM1evTowi7punzxxReKiIjQ6dOnXbrdBQsWKCIiQkeOHHHpdgvS9R5Dfr2nAP6HEAzcJDIyMhQREWH7qlu3rm6//Xb17t1bb731lg4dOpRtnfT0dO3evVvx8fFO7evkyZOKiIjQV1995dR6Oe0vNTVVu3fv1tmzZ53a1o3UeL3HXdCmTJmil156ScOGDdOCBQs0bNiwbH3mz5+viIgILVq0KNftnDx5UrfccotGjRqVn+XmKj4+Xrt371Z6erpLt3vu3Dnt3r1bqampLt3ujVi+fHm2n8O77rpLI0eO1PHjx7P1v95jyK/3FMD/eBZ2AQAcY4zR7t271alTJ73zzjuSpMTERO3atUszZ87UmDFjNHr0aP3f//2fbZ2goCDt3LlT5cuXd2pfaWlp2r17txISEpxa73r3dz3yqrEg67gRixcvVrNmzdSjR49c+7Rp00YxMTH68MMP1bVr1xz7zJgxQzt37tT777+fX6Xi/0tKStLu3bs1YcIEdenSRWlpadqyZYteeOEFffHFF9q0aZMqVqxo69+jRw/dfvvtqlq1aiFWDSAnhGDgJlO6dGlFRETYXjdr1kwDBw7U66+/rrFjxyowMFDPP/+8JMnDw8Oub34r6P0V9TquJTY2VtWrV8+zT0BAgO6//37NnDlTR44cUZUqVbL1+fTTTxUeHq42bdrkV6m4SmhoqO0zduutt8rPz089evTQxx9/bPcf0YCAAAUEBBRWmQDywHQIoJh4+eWXVadOHb3xxhtKSUmRlPvc2J9++kn333+/mjRponvvvVejRo3SqVOnJEmbNm3S3XffLUl64403bH/2feONNyTZz/Fdu3atevXqpVtvvVUrV6685lzcNWvWqEuXLmrYsKEefPBBbdu2zW75+vXrFRERoejo6Gzr1qtXTxMmTHCoxtzqSE9P18cff6z27durfv36ateunT788EO7PzlfeXx//vmnevTooQYNGuiBBx7Q9u3br3keHNnPypUrFRERof3799u+j4iI0N9//53j9h577DFlZmbqs88+y7Zs1apV2r17twYPHiw3NzdJUlxcnF544QW1aNFCDRs21P33369ffvkl27oXL17UpEmT1L59ezVs2FA9e/a0m3YRHR1tqy0yMlK33XabHnrooRzPT5apU6fqrrvuUpMmTTRy5Mhs02AmTJigevXqZVsva1/r16/PddvO1HTlnNpPP/3UNu86azrD8uXLs237r7/+UkREhObMmZNnDTm57bbbJEl79uyxa89tTvC13vurj6V169Zq3Lixnn/+eSUlJeV6rNfqm7Xvd955R23atFH9+vUVFRWV7WclJSVFU6ZMUYcOHdSoUSN17dpVU6dOtftZcaQPUKQZADeFtLQ0I8n06dMn1z7//Oc/jSSzatUqY4wxp06dMpLMpEmTbH0WLFhg3N3dzauvvmrWr19voqOjzdtvv23atm1rjDHm4sWLZuXKlUaSGTNmjNm5c6fZuXOniY2NNcYYs3fvXiPJPP744+a+... (line truncated to 2000 chars)
4635:       "text/plain": [
4636:        "<Figure size 800x500 with 1 Axes>"
4637:       ]
4638:      },
4639:      "metadata": {},
4640:      "output_type": "display_data"
4641:     }
4642:    ],
4643:    "source": [
4644:     "plt.figure(figsize=(8,5))\n",
4645:     "\n",
4646:     "plt.hist(\n",
4647:     "    amazon_df[amazon_df[\"label\"] == 0][\"vocab_richness\"],\n",
4648:     "    bins=40,\n",
4649:     "    alpha=0.6,\n",
4650:     "    label=\"Genuine\"\n",
4651:     ")\n",
4652:     "\n",
4653:     "plt.hist(\n",
4654:     "    amazon_df[amazon_df[\"label\"] == 1][\"vocab_richness\"],\n",
4655:     "    bins=40,\n",
4656:     "    alpha=0.6,\n",
4657:     "    label=\"AI Generated\"\n",
4658:     ")\n",
4659:     "\n",
4660:     "plt.xlabel(\"Vocabulary Richness\")\n",
4661:     "plt.ylabel(\"Frequency\")\n",
4662:     "plt.title(\"Distribution of Vocabulary Richness\")\n",
4663:     "plt.legend()\n",
4664:     "\n",
4665:     "plt.show()"
4666:    ]
4667:   },
4668:   {
4669:    "cell_type": "code",
4670:    "execution_count": 637,
4671:    "id": "de8cb41c",
4672:    "metadata": {},
4673:    "outputs": [
4674:     {
4675:      "data": {
4676:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAcsAAAF1CAYAAACHwsFCAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAT51JREFUeJzt3XdYFNf7NvCbjoWiqBTBYMQSRcWGDSsQxd6xF+wlBk0sqIk9GGP5Ro0NwY7daGwYO6goVgSNWCICFlSUJtLP+4cv83OlbGHJot6f69rrYs+cc+aZ3YGHM+WMlhBCgIiIiPKlrekAiIiIijsmSyIiIjmYLImIiORgsiQiIpKDyZKIiEgOJksiIiI5mCyJiIjkYLIkIiKSg8mSqBCOHTuGgwcPqr3fU6dOYe/evWrv97+k6jYU1WdaHHyK21YUMX+K+7cWZ/DRvJcvX+LgwYMwNTVFr169NB1OsXH48GG8fPkSQ4cOhZaWVp51Hj9+jBMnTqBZs2aoWbPmfxwh4OLigvj4eFy9elWt/fbq1Qvh4eG4e/euWvstjPPnz8vEo6+vDysrKzRr1gwlS5bMVV/VbSiqz7Q4+K+2Lee7Gjx4MPT19QvVV1HEXBz3b3k4siwG1qxZg5EjR8Ld3R2PHz/WdDjFxrVr1+Dh4YFz587lW2fx4sUYOXIkdHV1/8PIvkybNm3CyJEjERgYiEuXLuHIkSMYMmQIKlasiP379+eq7+Ligt69e2sgUsr5rlJSUjQdymeDyVLDsrOz4efnh06dOsHQ0BB+fn6aDqnY8PDwgLa2Nnx9ffNc/u7dO/j7+6Nly5aoVq3afxzdl2vFihXYsGEDdu3ahXv37sHGxgYDBw7Ey5cvZeqNGTMG8+fP11CUROrFf8c17MSJE3j8+DG2b98Oc3Nz+Pn54eeff4aOjg4A4J9//sGFCxfQtWtXlC9fXqZtcnIydu7ciYYNG8LBwUEqT0pKwvnz5/Hy5UtYWVmhRYsWMDAwkJbfvn0bwcHBGDBgAADg9OnTeP78OYYPH46YmBgEBAQAALS0tFCiRAnUrFlTpv8P3b59Gzdv3kS5cuXg7OyMFy9e4OjRo+jQoQOsrKxk6sqL62M2NjZo37499u3bh1WrVsHExERm+d69exEfH4+RI0fKlIeGhuL27dvQ0dFBo0aN8PXXX+fZ/5MnTxASEoK0tDQ4ODigRo0a0rLg4GDcvn0bAKCtrQ1TU1M4OjrC2to633gjIyMRHBwMIyMjtGnTBqVKlcoVr6mpKVxcXGTKg4ODce/ePQwZMiTfvpWJ6dixY0hPT0fXrl3x5MkTXLhwAaampgCAFy9eYODAgbn6vnPnDi5evIgePXqgbNmyBcbxoVKlSmHgwIGYNm0aAgMD0bNnT2nZqVOn8ObNmzxPLRT02X9cLygoCCVLlkTbtm1RunTpAre1oLo5oqKiEBISgtTUVNSsWRP169fPVScmJgY3btzA27dvUa1aNdSrVy/XqQBF6hSkoP3l77//Vvt39bGi2MdzKPIZf3IEaVTPnj1F3bp1hRBCXL9+XQAQhw8flpbfv39faGlpiQULFuRq6+PjIwCIS5cuSWXr1q0TRkZGok6dOsLd3V1Ur15d2NjYiCtXrkh1li9fLgCIEydOCAcHB9G9e3dRsWJFIYQQ4eHhYvjw4WL48OHCw8NDdOrUSZQsWVI0a9ZMJCUlSX1kZWWJUaNGCW1tbdGmTRvRpUsX0axZM7Ft2zap7w8pElde9u/fLwCIP/74I9eyVq1aCVNTU/Hu3TshhBCvXr0Szs7OolSpUqJTp06ibdu2Qk9PT3h4eIj09HSpXUpKihg2bJjQ1dUVzZs3F+7u7qJmzZqiW7duIjs7WwghxPbt26XPYciQIcLJyUno6OiI6dOny8Tg7OwsGjRoINatWyfq1q0revfuLWxsbISlpaUICQmRqVu9enXRtWvXXNsxfvx4UapUKZmynj17iurVq8uU... (line truncated to 2000 chars)
4677:       "text/plain": [
4678:        "<Figure size 500x400 with 1 Axes>"
4679:       ]
4680:      },
4681:      "metadata": {},
4682:      "output_type": "display_data"
4683:     }
4684:    ],
4685:    "source": [
4686:     "vocab_mean = amazon_df.groupby(\"label\")[\"vocab_richness\"].mean()\n",
4687:     "\n",
4688:     "plt.figure(figsize=(5,4))\n",
4689:     "\n",
4690:     "plt.bar(\n",
4691:     "    [\"Genuine\", \"AI Generated\"],\n",
4692:     "    vocab_mean.values,\n",
4693:     "    color=[\"#2E8B57\", \"#DC143C\"]\n",
4694:     ")\n",
4695:     "\n",
4696:     "plt.ylabel(\"Average Vocabulary Richness\")\n",
4697:     "plt.title(\"Average Vocabulary Richness by Label\")\n",
4698:     "\n",
4699:     "for i, value in enumerate(vocab_mean.values):\n",
4700:     "    plt.text(i, value, f\"{value:.3f}\", ha=\"center\", va=\"bottom\")\n",
4701:     "\n",
4702:     "plt.show()"
4703:    ]
4704:   },
4705:   {
4706:    "cell_type": "markdown",
4707:    "id": "2743b459",
4708:    "metadata": {},
4709:    "source": [
4710:     "This is interesting AI reviews have lower vocab richness than i thought would be the case.<br>\n",
4711:     "A guess i can take is in order to look like geniune ai generated review might delibratly reduce their own vocabulary.<br>\n",
4712:     "looking at the box plot and distribution graph. i believe my assumption is correct since human reviews didnt fall below a certain point(0.3). and even in the range of 0.3 there were very few examples which we can also rule as outliers."
4713:    ]
4714:   },
4715:   {
4716:    "cell_type": "code",
4717:    "execution_count": 633,
4718:    "id": "6cf166cb",
4719:    "metadata": {},
4720:    "outputs": [
4721:     {
4722:      "data": {
4723:       "text/html": [
4724:        "<div>\n",
4725:        "<style scoped>\n",
4726:        "    .dataframe tbody tr th:only-of-type {\n",
4727:        "        vertical-align: middle;\n",
4728:        "    }\n",
4729:        "\n",
4730:        "    .dataframe tbody tr th {\n",
4731:        "        vertical-align: top;\n",
4732:        "    }\n",
4733:        "\n",
4734:        "    .dataframe thead tr th {\n",
4735:        "        text-align: left;\n",
4736:        "    }\n",
4737:        "\n",
4738:        "    .dataframe thead tr:last-of-type th {\n",
4739:        "        text-align: right;\n",
4740:        "    }\n",
4741:        "</style>\n",
4742:        "<table border=\"1\" class=\"dataframe\">\n",
4743:        "  <thead>\n",
4744:        "    <tr>\n",
4745:        "      <th></th>\n",
4746:        "      <th colspan=\"8\" halign=\"left\">text_length</th>\n",
4747:        "      <th colspan=\"8\" halign=\"left\">word_count</th>\n",
4748:        "      <th colspan=\"8\" halign=\"left\">sentence_count</th>\n",
4749:        "      <th colspan=\"8\" halign=\"left\">avg_word_len</th>\n",
4750:        "      <th colspan=\"8\" halign=\"left\">vocab_richness</th>\n",
4751:        "    </tr>\n",
4752:        "    <tr>\n",
4753:        "      <th></th>\n",
4754:        "      <th>count</th>\n",
4755:        "      <th>mean</th>\n",
4756:        "      <th>std</th>\n",
4757:        "      <th>min</th>\n",
4758:        "      <th>25%</th>\n",
4759:        "      <th>50%</th>\n",
4760:        "      <th>75%</th>\n",
4761:        "      <th>max</th>\n",
4762:        "      <th>count</th>\n",
4763:        "      <th>mean</th>\n",
4764:        "      <th>std</th>\n",
4765:        "      <th>min</th>\n",
4766:        "      <th>25%</th>\n",
4767:        "      <th>50%</th>\n",
4768:        "      <th>75%</th>\n",
4769:        "      <th>max</th>\n",
4770:        "      <th>count</th>\n",
4771:        "      <th>mean</th>\n",
4772:        "      <th>std</th>\n",
4773:        "      <th>min</th>\n",
4774:        "      <th>25%</th>\n",
4775:        "      <th>50%</th>\n",
4776:        "      <th>75%</th>\n",
4777:        "      <th>max</th>\n",
4778:        "      <th>count</th>\n",
4779:        "      <th>mean</th>\n",
4780:        "      <th>std</th>\n",
4781:        "      <th>min</th>\n",
4782:        "      <th>25%</th>\n",
4783:        "      <th>50%</th>\n",
4784:        "      <th>75%</th>\n",
4785:        "      <th>max</th>\n",
4786:        "      <th>count</th>\n",
4787:        "      <th>mean</th>\n",
4788:        "      <th>std</th>\n",
4789:        "      <th>min</th>\n",
4790:        "      <th>25%</th>\n",
4791:        "      <th>50%</th>\n",
4792:        "      <th>75%</th>\n",
4793:        "      <th>max</th>\n",
4794:        "    </tr>\n",
4795:        "    <tr>\n",
4796:        "      <th>label</th>\n",
4797:        "      <th></th>\n",
4798:        "      <th></th>\n",
4799:        "      <th></th>\n",
4800:        "      <th></th>\n",
4801:        "      <th></th>\n",
4802:        "      <th></th>\n",
4803:        "      <th></th>\n",
4804:        "      <th></th>\n",
4805:        "      <th></th>\n",
4806:        "      <th></th>\n",
4807:        "      <th></th>\n",
4808:        "      <th></th>\n",
4809:        "      <th></th>\n",
4810:        "      <th></th>\n",
4811:        "      <th></th>\n",
4812:        "      <th></th>\n",
4813:        "      <th></th>\n",
4814:        "      <th></th>\n",
4815:        "      <th></th>\n",
4816:        "      <th></th>\n",
4817:        "      <th></th>\n",
4818:        "      <th></th>\n",
4819:        "      <th></th>\n",
4820:        "      <th></th>\n",
4821:        "      <th></th>\n",
4822:        "      <th></th>\n",
4823:        "      <th></th>\n",
4824:        "      <th></th>\n",

(Output capped at 50 KB. Showing lines 3826-4824. Use offset=4825 to continue.)
</content>
```

---

## User

---

## Assistant (Compaction · MiMo V2.5 Free · 18.7s)

_Thinking:_

Let me summarize the conversation carefully.

## Objective
- Help the user document their `cross-domain-V2.ipynb` notebook by advising on what markdown cells and comments to add — the user adds them manually, the agent advises on wording and placement.

## Important Details
- User wants documentation that is **not too heavy** — brief markdown cells, not verbose
- User prefers to write their own markdown after the agent frames/suggests wording
- The notebook is about **Cross-Domain Fake Review Detection** using Amazon and Yelp review datasets
- Pipeline flow: Data Loading → Label Encoding → Column Standardization → Duplicate Removal → Text Cleaning → Review Length Filtering → Class Balance/Balancing → EDA (distributions, word clouds, n-grams, correlations, summary stats) → Feature Engineering
- Label mapping: Amazon `CG`→1, `OR`→0; Yelp `-1`→1, `1`→0 (1=fake/AI-generated, 0=genuine)
- Short reviews (<20 chars) removed — user wants markdown explaining the rationale (AI text tends to be more complete/polished; short texts lack signal) without hardcoding the threshold
- Datasets: Amazon `fake reviews dataset.csv` (40,432 rows), Yelp `Labelled Yelp Dataset.csv` (359,052 rows); Yelp sampled to ~25k per class for balance

## Work State
### Completed
- Read and analyzed the full notebook structure
- Provided a comprehensive list of ~14 recommended markdown insertion points with suggested wording (title, label encoding, column standardization, duplicate removal, text cleaning, review length filtering, class distribution, balance Yelp, EDA, feature engineering, distributions, word clouds, n-grams, correlation, summary stats)
- Drafted polished wording for the review length filtering markdown cell

### Active
- User was reviewing the notebook again (re-read at user's request) to see what markdown they've already added and determine next steps
- The user's last message asked the agent to re-read the notebook to see current state and advise what to do next — the agent was mid-read when conversation ended

### Blocked
- Need to finish re-reading the notebook to see what markdown cells the user has already added and what's still missing

## Next Move
1. Finish re-reading the full notebook to inventory which markdown cells the user has already added vs. which recommended ones are still missing
2. Report back to the user with what's done and what remaining markdown/comment suggestions they should add next

## Relevant Files
- `/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb`: primary notebook being documented
- `/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/classical model-set-project.ipynb`: other notebook in repo (not being documented)

---

## User

---

## Assistant (Plan · MiMo V2.5 Free · 3.3s)

_Thinking:_

The user wants me to continue from where we left off. Based on the context, we were documenting a Jupyter notebook. I need to:

1. Re-read the notebook to see the current state of markdown cells
2. Report what's already done and what's still needed

Let me read the notebook first to understand what markdown cells already exist.

Let me re-read the notebook to see what markdown cells you've already added and what's still missing.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb"
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
1: {
2:  "cells": [
3:   {
4:    "cell_type": "code",
5:    "execution_count": 508,
6:    "id": "ceb271b9",
7:    "metadata": {},
8:    "outputs": [
9:     {
10:      "name": "stdout",
11:      "output_type": "stream",
12:      "text": [
13:       "Amazon shape: (40432, 4)\n",
14:       "Yelp shape: (359052, 6)\n"
15:      ]
16:     }
17:    ],
18:    "source": [
19:     "import pandas as pd\n",
20:     "import numpy as np\n",
21:     "import re\n",
22:     "from sklearn.utils import resample\n",
23:     "from sklearn.model_selection import train_test_split\n",
24:     "from sklearn.metrics import accuracy_score\n",
25:     "import nltk\n",
26:     "from nltk.corpus import stopwords\n",
27:     "from nltk.stem import PorterStemmer\n",
28:     "\n",
29:     "# Load datasets\n",
30:     "amazon_df = pd.read_csv('fake reviews dataset.csv')\n",
31:     "yelp_df = pd.read_csv('Labelled Yelp Dataset.csv')\n",
32:     "\n",
33:     "# Quick view\n",
34:     "print(\"Amazon shape:\", amazon_df.shape)\n",
35:     "print(\"Yelp shape:\", yelp_df.shape)\n"
36:    ]
37:   },
38:   {
39:    "cell_type": "code",
40:    "execution_count": 509,
41:    "id": "aa9d3b06",
42:    "metadata": {},
43:    "outputs": [],
44:    "source": [
45:     "pd.set_option(\"display.max_columns\", None)\n",
46:     "pd.set_option(\"display.max_colwidth\", 200)"
47:    ]
48:   },
49:   {
50:    "cell_type": "code",
51:    "execution_count": 510,
52:    "id": "55238bc3",
53:    "metadata": {},
54:    "outputs": [
55:     {
56:      "data": {
57:       "text/html": [
58:        "<div>\n",
59:        "<style scoped>\n",
60:        "    .dataframe tbody tr th:only-of-type {\n",
61:        "        vertical-align: middle;\n",
62:        "    }\n",
63:        "\n",
64:        "    .dataframe tbody tr th {\n",
65:        "        vertical-align: top;\n",
66:        "    }\n",
67:        "\n",
68:        "    .dataframe thead th {\n",
69:        "        text-align: right;\n",
70:        "    }\n",
71:        "</style>\n",
72:        "<table border=\"1\" class=\"dataframe\">\n",
73:        "  <thead>\n",
74:        "    <tr style=\"text-align: right;\">\n",
75:        "      <th></th>\n",
76:        "      <th>category</th>\n",
77:        "      <th>rating</th>\n",
78:        "      <th>label</th>\n",
79:        "      <th>text_</th>\n",
80:        "    </tr>\n",
81:        "  </thead>\n",
82:        "  <tbody>\n",
83:        "    <tr>\n",
84:        "      <th>0</th>\n",
85:        "      <td>Home_and_Kitchen_5</td>\n",
86:        "      <td>5.0</td>\n",
87:        "      <td>CG</td>\n",
88:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
89:        "    </tr>\n",
90:        "    <tr>\n",
91:        "      <th>1</th>\n",
92:        "      <td>Home_and_Kitchen_5</td>\n",
93:        "      <td>5.0</td>\n",
94:        "      <td>CG</td>\n",
95:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
96:        "    </tr>\n",
97:        "    <tr>\n",
98:        "      <th>2</th>\n",
99:        "      <td>Home_and_Kitchen_5</td>\n",
100:        "      <td>5.0</td>\n",
101:        "      <td>CG</td>\n",
102:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
103:        "    </tr>\n",
104:        "    <tr>\n",
105:        "      <th>3</th>\n",
106:        "      <td>Home_and_Kitchen_5</td>\n",
107:        "      <td>1.0</td>\n",
108:        "      <td>CG</td>\n",
109:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
110:        "    </tr>\n",
111:        "    <tr>\n",
112:        "      <th>4</th>\n",
113:        "      <td>Home_and_Kitchen_5</td>\n",
114:        "      <td>5.0</td>\n",
115:        "      <td>CG</td>\n",
116:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
117:        "    </tr>\n",
118:        "  </tbody>\n",
119:        "</table>\n",
120:        "</div>"
121:       ],
122:       "text/plain": [
123:        "             category  rating label  \\\n",
124:        "0  Home_and_Kitchen_5     5.0    CG   \n",
125:        "1  Home_and_Kitchen_5     5.0    CG   \n",
126:        "2  Home_and_Kitchen_5     5.0    CG   \n",
127:        "3  Home_and_Kitchen_5     1.0    CG   \n",
128:        "4  Home_and_Kitchen_5     5.0    CG   \n",
129:        "\n",
130:        "                                                                                   text_  \n",
131:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty  \n",
132:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years  \n",
133:        "2                    This pillow saved my back. I love the look and feel of this pillow.  \n",
134:        "3      Missing information on how to use it, but it is a great product for the price!  I  \n",
135:        "4  Very nice set. Good quality. We have had the set for two months now and have not been  "
136:       ]
137:      },
138:      "execution_count": 510,
139:      "metadata": {},
140:      "output_type": "execute_result"
141:     }
142:    ],
143:    "source": [
144:     "amazon_df.head()"
145:    ]
146:   },
147:   {
148:    "cell_type": "code",
149:    "execution_count": 511,
150:    "id": "7800c77e",
151:    "metadata": {},
152:    "outputs": [
153:     {
154:      "data": {
155:       "text/html": [
156:        "<div>\n",
157:        "<style scoped>\n",
158:        "    .dataframe tbody tr th:only-of-type {\n",
159:        "        vertical-align: middle;\n",
160:        "    }\n",
161:        "\n",
162:        "    .dataframe tbody tr th {\n",
163:        "        vertical-align: top;\n",
164:        "    }\n",
165:        "\n",
166:        "    .dataframe thead th {\n",
167:        "        text-align: right;\n",
168:        "    }\n",
169:        "</style>\n",
170:        "<table border=\"1\" class=\"dataframe\">\n",
171:        "  <thead>\n",
172:        "    <tr style=\"text-align: right;\">\n",
173:        "      <th></th>\n",
174:        "      <th>User_id</th>\n",
175:        "      <th>Product_id</th>\n",
176:        "      <th>Rating</th>\n",
177:        "      <th>Date</th>\n",
178:        "      <th>Review</th>\n",
179:        "      <th>Label</th>\n",
180:        "    </tr>\n",
181:        "  </thead>\n",
182:        "  <tbody>\n",
183:        "    <tr>\n",
184:        "      <th>0</th>\n",
185:        "      <td>923</td>\n",
186:        "      <td>0</td>\n",
187:        "      <td>3</td>\n",
188:        "      <td>12/8/2014</td>\n",
189:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
190:        "      <td>-1</td>\n",
191:        "    </tr>\n",
192:        "    <tr>\n",
193:        "      <th>1</th>\n",
194:        "      <td>924</td>\n",
195:        "      <td>0</td>\n",
196:        "      <td>3</td>\n",
197:        "      <td>5/16/2013</td>\n",
198:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
199:        "      <td>-1</td>\n",
200:        "    </tr>\n",
201:        "    <tr>\n",
202:        "      <th>2</th>\n",
203:        "      <td>925</td>\n",
204:        "      <td>0</td>\n",
205:        "      <td>4</td>\n",
206:        "      <td>7/1/2013</td>\n",
207:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
208:        "      <td>-1</td>\n",
209:        "    </tr>\n",
210:        "    <tr>\n",
211:        "      <th>3</th>\n",
212:        "      <td>926</td>\n",
213:        "      <td>0</td>\n",
214:        "      <td>4</td>\n",
215:        "      <td>7/28/2011</td>\n",
216:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
217:        "      <td>-1</td>\n",
218:        "    </tr>\n",
219:        "    <tr>\n",
220:        "      <th>4</th>\n",
221:        "      <td>927</td>\n",
222:        "      <td>0</td>\n",
223:        "      <td>4</td>\n",
224:        "      <td>11/1/2010</td>\n",
225:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
226:        "      <td>-1</td>\n",
227:        "    </tr>\n",
228:        "  </tbody>\n",
229:        "</table>\n",
230:        "</div>"
231:       ],
232:       "text/plain": [
233:        "   User_id  Product_id  Rating       Date  \\\n",
234:        "0      923           0       3  12/8/2014   \n",
235:        "1      924           0       3  5/16/2013   \n",
236:        "2      925           0       4   7/1/2013   \n",
237:        "3      926           0       4  7/28/2011   \n",
238:        "4      927           0       4  11/1/2010   \n",
239:        "\n",
240:        "                                                                                                                                                                                                    Review  \\\n",
241:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
242:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
243:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
244:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
245:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
246:        "\n",
247:        "   Label  \n",
248:        "0     -1  \n",
249:        "1     -1  \n",
250:        "2     -1  \n",
251:        "3     -1  \n",
252:        "4     -1  "
253:       ]
254:      },
255:      "execution_count": 511,
256:      "metadata": {},
257:      "output_type": "execute_result"
258:     }
259:    ],
260:    "source": [
261:     "yelp_df.head()"
262:    ]
263:   },
264:   {
265:    "cell_type": "code",
266:    "execution_count": 512,
267:    "id": "9af9b883",
268:    "metadata": {},
269:    "outputs": [
270:     {
271:      "name": "stdout",
272:      "output_type": "stream",
273:      "text": [
274:       "Column Names:\n",
275:       "\n",
276:       "['category', 'rating', 'label', 'text_']\n",
277:       "\n",
278:       "Dataset Info:\n",
279:       "\n",
280:       "<class 'pandas.DataFrame'>\n",
281:       "RangeIndex: 40432 entries, 0 to 40431\n",
282:       "Data columns (total 4 columns):\n",
283:       " #   Column    Non-Null Count  Dtype  \n",
284:       "---  ------    --------------  -----  \n",
285:       " 0   category  40432 non-null  str    \n",
286:       " 1   rating    40432 non-null  float64\n",
287:       " 2   label     40432 non-null  str    \n",
288:       " 3   text_     40432 non-null  str    \n",
289:       "dtypes: float64(1), str(3)\n",
290:       "memory usage: 15.5 MB\n",
291:       "\n",
292:       "Missing Values:\n",
293:       "\n",
294:       "category    0\n",
295:       "rating      0\n",
296:       "label       0\n",
297:       "text_       0\n",
298:       "dtype: int64\n"
299:      ]
300:     }
301:    ],
302:    "source": [
303:     "print(\"Column Names:\\n\")\n",
304:     "print(amazon_df.columns.tolist())\n",
305:     "\n",
306:     "print(\"\\nDataset Info:\\n\")\n",
307:     "amazon_df.info()\n",
308:     "\n",
309:     "print(\"\\nMissing Values:\\n\")\n",
310:     "print(amazon_df.isnull().sum())"
311:    ]
312:   },
313:   {
314:    "cell_type": "code",
315:    "execution_count": 513,
316:    "id": "f9678399",
317:    "metadata": {},
318:    "outputs": [
319:     {
320:      "name": "stdout",
321:      "output_type": "stream",
322:      "text": [
323:       "Column Names:\n",
324:       "\n",
325:       "['User_id', 'Product_id', 'Rating', 'Date', 'Review', 'Label']\n",
326:       "\n",
327:       "Dataset Info:\n",
328:       "\n",
329:       "<class 'pandas.DataFrame'>\n",
330:       "RangeIndex: 359052 entries, 0 to 359051\n",
331:       "Data columns (total 6 columns):\n",
332:       " #   Column      Non-Null Count   Dtype\n",
333:       "---  ------      --------------   -----\n",
334:       " 0   User_id     359052 non-null  int64\n",
335:       " 1   Product_id  359052 non-null  int64\n",
336:       " 2   Rating      359052 non-null  int64\n",
337:       " 3   Date        359052 non-null  str  \n",
338:       " 4   Review      359052 non-null  str  \n",
339:       " 5   Label       359052 non-null  int64\n",
340:       "dtypes: int64(4), str(2)\n",
341:       "memory usage: 239.0 MB\n",
342:       "\n",
343:       "Missing Values:\n",
344:       "\n",
345:       "User_id       0\n",
346:       "Product_id    0\n",
347:       "Rating        0\n",
348:       "Date          0\n",
349:       "Review        0\n",
350:       "Label         0\n",
351:       "dtype: int64\n"
352:      ]
353:     }
354:    ],
355:    "source": [
356:     "print(\"Column Names:\\n\")\n",
357:     "print(yelp_df.columns.tolist())\n",
358:     "\n",
359:     "print(\"\\nDataset Info:\\n\")\n",
360:     "yelp_df.info()\n",
361:     "\n",
362:     "print(\"\\nMissing Values:\\n\")\n",
363:     "print(yelp_df.isnull().sum())"
364:    ]
365:   },
366:   {
367:    "cell_type": "markdown",
368:    "id": "9c6f6dbe",
369:    "metadata": {},
370:    "source": [
371:     "### Label Encoding"
372:    ]
373:   },
374:   {
375:    "cell_type": "markdown",
376:    "id": "9ba41eba",
377:    "metadata": {},
378:    "source": [
379:     " 1 = fake/AI-generated, 0 = genuine"
380:    ]
381:   },
382:   {
383:    "cell_type": "code",
384:    "execution_count": 514,
385:    "id": "d9a08569",
386:    "metadata": {},
387:    "outputs": [
388:     {
389:      "data": {
390:       "text/html": [
391:        "<div>\n",
392:        "<style scoped>\n",
393:        "    .dataframe tbody tr th:only-of-type {\n",
394:        "        vertical-align: middle;\n",
395:        "    }\n",
396:        "\n",
397:        "    .dataframe tbody tr th {\n",
398:        "        vertical-align: top;\n",
399:        "    }\n",
400:        "\n",
401:        "    .dataframe thead th {\n",
402:        "        text-align: right;\n",
403:        "    }\n",
404:        "</style>\n",
405:        "<table border=\"1\" class=\"dataframe\">\n",
406:        "  <thead>\n",
407:        "    <tr style=\"text-align: right;\">\n",
408:        "      <th></th>\n",
409:        "      <th>category</th>\n",
410:        "      <th>rating</th>\n",
411:        "      <th>label</th>\n",
412:        "      <th>text_</th>\n",
413:        "    </tr>\n",
414:        "  </thead>\n",
415:        "  <tbody>\n",
416:        "    <tr>\n",
417:        "      <th>0</th>\n",
418:        "      <td>Home_and_Kitchen_5</td>\n",
419:        "      <td>5.0</td>\n",
420:        "      <td>1</td>\n",
421:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
422:        "    </tr>\n",
423:        "    <tr>\n",
424:        "      <th>1</th>\n",
425:        "      <td>Home_and_Kitchen_5</td>\n",
426:        "      <td>5.0</td>\n",
427:        "      <td>1</td>\n",
428:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
429:        "    </tr>\n",
430:        "    <tr>\n",
431:        "      <th>2</th>\n",
432:        "      <td>Home_and_Kitchen_5</td>\n",
433:        "      <td>5.0</td>\n",
434:        "      <td>1</td>\n",
435:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
436:        "    </tr>\n",
437:        "    <tr>\n",
438:        "      <th>3</th>\n",
439:        "      <td>Home_and_Kitchen_5</td>\n",
440:        "      <td>1.0</td>\n",
441:        "      <td>1</td>\n",
442:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
443:        "    </tr>\n",
444:        "    <tr>\n",
445:        "      <th>4</th>\n",
446:        "      <td>Home_and_Kitchen_5</td>\n",
447:        "      <td>5.0</td>\n",
448:        "      <td>1</td>\n",
449:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
450:        "    </tr>\n",
451:        "  </tbody>\n",
452:        "</table>\n",
453:        "</div>"
454:       ],
455:       "text/plain": [
456:        "             category  rating  label  \\\n",
457:        "0  Home_and_Kitchen_5     5.0      1   \n",
458:        "1  Home_and_Kitchen_5     5.0      1   \n",
459:        "2  Home_and_Kitchen_5     5.0      1   \n",
460:        "3  Home_and_Kitchen_5     1.0      1   \n",
461:        "4  Home_and_Kitchen_5     5.0      1   \n",
462:        "\n",
463:        "                                                                                   text_  \n",
464:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty  \n",
465:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years  \n",
466:        "2                    This pillow saved my back. I love the look and feel of this pillow.  \n",
467:        "3      Missing information on how to use it, but it is a great product for the price!  I  \n",
468:        "4  Very nice set. Good quality. We have had the set for two months now and have not been  "
469:       ]
470:      },
471:      "execution_count": 514,
472:      "metadata": {},
473:      "output_type": "execute_result"
474:     }
475:    ],
476:    "source": [
477:     "label_map={'CG':1,'OR':0}\n",
478:     "amazon_df['label']=amazon_df['label'].map(label_map)\n",
479:     "amazon_df.head()"
480:    ]
481:   },
482:   {
483:    "cell_type": "markdown",
484:    "id": "4a3ccf6b",
485:    "metadata": {},
486:    "source": [
487:     " ### Column Standardization"
488:    ]
489:   },
490:   {
491:    "cell_type": "code",
492:    "execution_count": 515,
493:    "id": "489d777d",
494:    "metadata": {},
495:    "outputs": [
496:     {
497:      "data": {
498:       "text/html": [
499:        "<div>\n",
500:        "<style scoped>\n",
501:        "    .dataframe tbody tr th:only-of-type {\n",
502:        "        vertical-align: middle;\n",
503:        "    }\n",
504:        "\n",
505:        "    .dataframe tbody tr th {\n",
506:        "        vertical-align: top;\n",
507:        "    }\n",
508:        "\n",
509:        "    .dataframe thead th {\n",
510:        "        text-align: right;\n",
511:        "    }\n",
512:        "</style>\n",
513:        "<table border=\"1\" class=\"dataframe\">\n",
514:        "  <thead>\n",
515:        "    <tr style=\"text-align: right;\">\n",
516:        "      <th></th>\n",
517:        "      <th>rating</th>\n",
518:        "      <th>review</th>\n",
519:        "      <th>label</th>\n",
520:        "    </tr>\n",
521:        "  </thead>\n",
522:        "  <tbody>\n",
523:        "    <tr>\n",
524:        "      <th>0</th>\n",
525:        "      <td>5.0</td>\n",
526:        "      <td>Love this!&nbsp;&nbsp;Well made, sturdy, and very comfortable.&nbsp;&nbsp;I love it!Very pretty</td>\n",
527:        "      <td>1</td>\n",
528:        "    </tr>\n",
529:        "    <tr>\n",
530:        "      <th>1</th>\n",
531:        "      <td>5.0</td>\n",
532:        "      <td>love it, a great upgrade from the original.&nbsp;&nbsp;I've had mine for a couple of years</td>\n",
533:        "      <td>1</td>\n",
534:        "    </tr>\n",
535:        "    <tr>\n",
536:        "      <th>2</th>\n",
537:        "      <td>5.0</td>\n",
538:        "      <td>This pillow saved my back. I love the look and feel of this pillow.</td>\n",
539:        "      <td>1</td>\n",
540:        "    </tr>\n",
541:        "    <tr>\n",
542:        "      <th>3</th>\n",
543:        "      <td>1.0</td>\n",
544:        "      <td>Missing information on how to use it, but it is a great product for the price!&nbsp;&nbsp;I</td>\n",
545:        "      <td>1</td>\n",
546:        "    </tr>\n",
547:        "    <tr>\n",
548:        "      <th>4</th>\n",
549:        "      <td>5.0</td>\n",
550:        "      <td>Very nice set. Good quality. We have had the set for two months now and have not been</td>\n",
551:        "      <td>1</td>\n",
552:        "    </tr>\n",
553:        "  </tbody>\n",
554:        "</table>\n",
555:        "</div>"
556:       ],
557:       "text/plain": [
558:        "   rating  \\\n",
559:        "0     5.0   \n",
560:        "1     5.0   \n",
561:        "2     5.0   \n",
562:        "3     1.0   \n",
563:        "4     5.0   \n",
564:        "\n",
565:        "                                                                                  review  \\\n",
566:        "0            Love this!  Well made, sturdy, and very comfortable.  I love it!Very pretty   \n",
567:        "1       love it, a great upgrade from the original.  I've had mine for a couple of years   \n",
568:        "2                    This pillow saved my back. I love the look and feel of this pillow.   \n",
569:        "3      Missing information on how to use it, but it is a great product for the price!  I   \n",
570:        "4  Very nice set. Good quality. We have had the set for two months now and have not been   \n",
571:        "\n",
572:        "   label  \n",
573:        "0      1  \n",
574:        "1      1  \n",
575:        "2      1  \n",
576:        "3      1  \n",
577:        "4      1  "
578:       ]
579:      },
580:      "execution_count": 515,
581:      "metadata": {},
582:      "output_type": "execute_result"
583:     }
584:    ],
585:    "source": [
586:     "#Amazon rename and remove unwanted columns\n",
587:     "\n",
588:     "amazon_df = amazon_df.rename(columns={\n",
589:     "    \"text_\": \"review\"\n",
590:     "})\n",
591:     " \n",
592:     "amazon_df = amazon_df[[\"rating\",\"review\",\"label\"]]\n",
593:     "\n",
594:     "amazon_df.head()"
595:    ]
596:   },
597:   {
598:    "cell_type": "code",
599:    "execution_count": 516,
600:    "id": "a652d43b",
601:    "metadata": {},
602:    "outputs": [
603:     {
604:      "data": {
605:       "text/html": [
606:        "<div>\n",
607:        "<style scoped>\n",
608:        "    .dataframe tbody tr th:only-of-type {\n",
609:        "        vertical-align: middle;\n",
610:        "    }\n",
611:        "\n",
612:        "    .dataframe tbody tr th {\n",
613:        "        vertical-align: top;\n",
614:        "    }\n",
615:        "\n",
616:        "    .dataframe thead th {\n",
617:        "        text-align: right;\n",
618:        "    }\n",
619:        "</style>\n",
620:        "<table border=\"1\" class=\"dataframe\">\n",
621:        "  <thead>\n",
622:        "    <tr style=\"text-align: right;\">\n",
623:        "      <th></th>\n",
624:        "      <th>rating</th>\n",
625:        "      <th>review</th>\n",
626:        "      <th>label</th>\n",
627:        "    </tr>\n",
628:        "  </thead>\n",
629:        "  <tbody>\n",
630:        "    <tr>\n",
631:        "      <th>0</th>\n",
632:        "      <td>3</td>\n",
633:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
634:        "      <td>-1</td>\n",
635:        "    </tr>\n",
636:        "    <tr>\n",
637:        "      <th>1</th>\n",
638:        "      <td>3</td>\n",
639:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
640:        "      <td>-1</td>\n",
641:        "    </tr>\n",
642:        "    <tr>\n",
643:        "      <th>2</th>\n",
644:        "      <td>4</td>\n",
645:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
646:        "      <td>-1</td>\n",
647:        "    </tr>\n",
648:        "    <tr>\n",
649:        "      <th>3</th>\n",
650:        "      <td>4</td>\n",
651:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
652:        "      <td>-1</td>\n",
653:        "    </tr>\n",
654:        "    <tr>\n",
655:        "      <th>4</th>\n",
656:        "      <td>4</td>\n",
657:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
658:        "      <td>-1</td>\n",
659:        "    </tr>\n",
660:        "  </tbody>\n",
661:        "</table>\n",
662:        "</div>"
663:       ],
664:       "text/plain": [
665:        "   rating  \\\n",
666:        "0       3   \n",
667:        "1       3   \n",
668:        "2       4   \n",
669:        "3       4   \n",
670:        "4       4   \n",
671:        "\n",
672:        "                                                                                                                                                                                                    review  \\\n",
673:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
674:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
675:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
676:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
677:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
678:        "\n",
679:        "   label  \n",
680:        "0     -1  \n",
681:        "1     -1  \n",
682:        "2     -1  \n",
683:        "3     -1  \n",
684:        "4     -1  "
685:       ]
686:      },
687:      "execution_count": 516,
688:      "metadata": {},
689:      "output_type": "execute_result"
690:     }
691:    ],
692:    "source": [
693:     "#Yelp rename and remove unwanted columns\n",
694:     "\n",
695:     "yelp_df=yelp_df.rename(columns={\n",
696:     "    \"Rating\":\"rating\",\n",
697:     "    \"Review\":\"review\",\n",
698:     "    \"Label\":\"label\"\n",
699:     "})\n",
700:     "\n",
701:     "yelp_df=yelp_df[[\"rating\",\"review\",\"label\"]]\n",
702:     "\n",
703:     "yelp_df.head()"
704:    ]
705:   },
706:   {
707:    "cell_type": "code",
708:    "execution_count": 517,
709:    "id": "23166f6e",
710:    "metadata": {},
711:    "outputs": [
712:     {
713:      "data": {
714:       "text/html": [
715:        "<div>\n",
716:        "<style scoped>\n",
717:        "    .dataframe tbody tr th:only-of-type {\n",
718:        "        vertical-align: middle;\n",
719:        "    }\n",
720:        "\n",
721:        "    .dataframe tbody tr th {\n",
722:        "        vertical-align: top;\n",
723:        "    }\n",
724:        "\n",
725:        "    .dataframe thead th {\n",
726:        "        text-align: right;\n",
727:        "    }\n",
728:        "</style>\n",
729:        "<table border=\"1\" class=\"dataframe\">\n",
730:        "  <thead>\n",
731:        "    <tr style=\"text-align: right;\">\n",
732:        "      <th></th>\n",
733:        "      <th>rating</th>\n",
734:        "      <th>review</th>\n",
735:        "      <th>label</th>\n",
736:        "    </tr>\n",
737:        "  </thead>\n",
738:        "  <tbody>\n",
739:        "    <tr>\n",
740:        "      <th>0</th>\n",
741:        "      <td>3</td>\n",
742:        "      <td>The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...</td>\n",
743:        "      <td>1</td>\n",
744:        "    </tr>\n",
745:        "    <tr>\n",
746:        "      <th>1</th>\n",
747:        "      <td>3</td>\n",
748:        "      <td>This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...</td>\n",
749:        "      <td>1</td>\n",
750:        "    </tr>\n",
751:        "    <tr>\n",
752:        "      <th>2</th>\n",
753:        "      <td>4</td>\n",
754:        "      <td>ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.</td>\n",
755:        "      <td>1</td>\n",
756:        "    </tr>\n",
757:        "    <tr>\n",
758:        "      <th>3</th>\n",
759:        "      <td>4</td>\n",
760:        "      <td>This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...</td>\n",
761:        "      <td>1</td>\n",
762:        "    </tr>\n",
763:        "    <tr>\n",
764:        "      <th>4</th>\n",
765:        "      <td>4</td>\n",
766:        "      <td>Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...</td>\n",
767:        "      <td>1</td>\n",
768:        "    </tr>\n",
769:        "  </tbody>\n",
770:        "</table>\n",
771:        "</div>"
772:       ],
773:       "text/plain": [
774:        "   rating  \\\n",
775:        "0       3   \n",
776:        "1       3   \n",
777:        "2       4   \n",
778:        "3       4   \n",
779:        "4       4   \n",
780:        "\n",
781:        "                                                                                                                                                                                                    review  \\\n",
782:        "0  The food at snack is a selection of popular Greek dishes. The appetizer tray is good as is the Greek salad. We were underwhelmed with the main courses. There are 4-5 tables here so it's sometimes ...   \n",
783:        "1  This little place in Soho is wonderful. I had a lamb sandwich and a glass of wine. The price shocked me for how small the serving was, but then again, this is Soho. The staff can be a little snott...   \n",
784:        "2                     ordered lunch for 15 from Snack last Friday. Â On time, nothing missing and the food was great. Â I have added it to the regular company lunch list, as everyone enjoyed their meal.   \n",
785:        "3  This is a beautiful quaint little restaurant on a pretty street. Â If you're strolling through soho around lunchtime, this would be a great place to stop for a bite. I heard the reviews about the ...   \n",
786:        "4  Snack is great place for a Â casual sit down lunch- especially on a cold winter day. Â In many ways the restaurant mirrors the food- simple yet unique. Â The avgolemono soup was lemony perfection ...   \n",
787:        "\n",
788:        "   label  \n",
789:        "0      1  \n",
790:        "1      1  \n",
791:        "2      1  \n",
792:        "3      1  \n",
793:        "4      1  "
794:       ]
795:      },
796:      "execution_count": 517,
797:      "metadata": {},
798:      "output_type": "execute_result"
799:     }
800:    ],
801:    "source": [
802:     "label_map={-1:1,1:0}\n",
803:     "yelp_df['label']=yelp_df['label'].map(label_map)\n",
804:     "yelp_df.head()"
805:    ]
806:   },
807:   {
808:    "cell_type": "code",
809:    "execution_count": 518,
810:    "id": "1e220dea",
811:    "metadata": {},
812:    "outputs": [
813:     {
814:      "name": "stdout",
815:      "output_type": "stream",
816:      "text": [
817:       "<class 'pandas.DataFrame'>\n",
818:       "RangeIndex: 40432 entries, 0 to 40431\n",
819:       "Data columns (total 3 columns):\n",
820:       " #   Column  Non-Null Count  Dtype  \n",
821:       "---  ------  --------------  -----  \n",
822:       " 0   rating  40432 non-null  float64\n",
823:       " 1   review  40432 non-null  str    \n",
824:       " 2   label   40432 non-null  int64  \n",
825:       "dtypes: float64(1), int64(1), str(1)\n",
826:       "memory usage: 14.5 MB\n"
827:      ]
828:     }
829:    ],
830:    "source": [
831:     "amazon_df.info()"
832:    ]
833:   },
834:   {
835:    "cell_type": "code",
836:    "execution_count": 519,
837:    "id": "f27d1399",
838:    "metadata": {},
839:    "outputs": [
840:     {
841:      "data": {
842:       "text/plain": [
843:        "array([5., 1., 3., 2., 4.])"
844:       ]
845:      },
846:      "execution_count": 519,
847:      "metadata": {},
848:      "output_type": "execute_result"
849:     }
850:    ],
851:    "source": [
852:     "amazon_df[\"rating\"].unique()"
853:    ]
854:   },
855:   {
856:    "cell_type": "code",
857:    "execution_count": 520,
858:    "id": "edf61ac9",
859:    "metadata": {},
860:    "outputs": [],
861:    "source": [
862:     "amazon_df[\"rating\"]=amazon_df[\"rating\"].astype(int)"
863:    ]
864:   },
865:   {
866:    "cell_type": "code",
867:    "execution_count": 521,
868:    "id": "7b4ed1e5",
869:    "metadata": {},
870:    "outputs": [
871:     {
872:      "name": "stdout",
873:      "output_type": "stream",
874:      "text": [
875:       "<class 'pandas.DataFrame'>\n",
876:       "RangeIndex: 359052 entries, 0 to 359051\n",
877:       "Data columns (total 3 columns):\n",
878:       " #   Column  Non-Null Count   Dtype\n",
879:       "---  ------  --------------   -----\n",
880:       " 0   rating  359052 non-null  int64\n",
881:       " 1   review  359052 non-null  str  \n",
882:       " 2   label   359052 non-null  int64\n",
883:       "dtypes: int64(2), str(1)\n",
884:       "memory usage: 227.7 MB\n"
885:      ]
886:     }
887:    ],
888:    "source": [
889:     "yelp_df.info()"
890:    ]
891:   },
892:   {
893:    "cell_type": "markdown",
894:    "id": "a45750ff",
895:    "metadata": {},
896:    "source": [
897:     "### Duplicate Removal"
898:    ]
899:   },
900:   {
901:    "cell_type": "code",
902:    "execution_count": 522,
903:    "id": "eb911bf5",
904:    "metadata": {},
905:    "outputs": [
906:     {
907:      "name": "stdout",
908:      "output_type": "stream",
909:      "text": [
910:       "Duplicates Before: 12\n"
911:      ]
912:     }
913:    ],
914:    "source": [
915:     "print(\"Duplicates Before:\", amazon_df.duplicated().sum())"
916:    ]
917:   },
918:   {
919:    "cell_type": "code",
920:    "execution_count": 523,
921:    "id": "09285ccc",
922:    "metadata": {},
923:    "outputs": [
924:     {
925:      "name": "stdout",
926:      "output_type": "stream",
927:      "text": [
928:       "Dataset Shape After Removing Duplicates: (40412, 3)\n"
929:      ]
930:     }
931:    ],
932:    "source": [
933:     "amazon_df = amazon_df.drop_duplicates(subset=\"review\").reset_index(drop=True)\n",
934:     "\n",
935:     "print(\"Dataset Shape After Removing Duplicates:\", amazon_df.shape)"
936:    ]
937:   },
938:   {
939:    "cell_type": "code",
940:    "execution_count": 524,
941:    "id": "579a79b2",
942:    "metadata": {},
943:    "outputs": [
944:     {
945:      "name": "stdout",
946:      "output_type": "stream",
947:      "text": [
948:       "Duplicates Before: 469\n"
949:      ]
950:     }
951:    ],
952:    "source": [
953:     "print(\"Duplicates Before:\", yelp_df.duplicated().sum())"
954:    ]
955:   },
956:   {
957:    "cell_type": "code",
958:    "execution_count": 525,
959:    "id": "e16e34e8",
960:    "metadata": {},
961:    "outputs": [
962:     {
963:      "name": "stdout",
964:      "output_type": "stream",
965:      "text": [
966:       "Dataset Shape After Removing Duplicates: (358156, 3)\n"
967:      ]
968:     }
969:    ],
970:    "source": [
971:     "yelp_df = yelp_df.drop_duplicates(subset=\"review\").reset_index(drop=True)\n",
972:     "\n",
973:     "print(\"Dataset Shape After Removing Duplicates:\", yelp_df.shape)"
974:    ]
975:   },
976:   {
977:    "cell_type": "markdown",
978:    "id": "d6663b71",
979:    "metadata": {},
980:    "source": [
981:     "### Text Cleaning"
982:    ]
983:   },
984:   {
985:    "cell_type": "code",
986:    "execution_count": 526,
987:    "id": "2fe0a1b8",
988:    "metadata": {},
989:    "outputs": [],
990:    "source": [
991:     "def count_patterns(df, column):\n",
992:     "    # Convert column to string (ignore NaN issues)\n",
993:     "    text = df[column].fillna(\"\").astype(str)\n",
994:     "\n",
995:     "    html_count = text.str.contains(r\"<.*?>\", regex=True).sum()\n",
996:     "    url_count = text.str.contains(r\"http\\S+|www\\.\\S+\", regex=True).sum()\n",
997:     "    email_count = text.str.contains(r\"\\S+@\\S+\", regex=True).sum()\n",
998:     "\n",
999:     "    print(f\"Total rows: {len(df)}\")\n",
1000:     "    print(f\"Rows with HTML tags   : {html_count}\")\n",
1001:     "    print(f\"Rows with URLs        : {url_count}\")\n",
1002:     "    print(f\"Rows with Email IDs   : {email_count}\")\n",
1003:     "\n",
1004:     "    return {\n",
1005:     "        \"html_tags\": html_count,\n",
1006:     "        \"urls\": url_count,\n",
1007:     "        \"emails\": email_count\n",
1008:     "    }"
1009:    ]
1010:   },
1011:   {
1012:    "cell_type": "code",
1013:    "execution_count": 527,
1014:    "id": "b083f438",
1015:    "metadata": {},
1016:    "outputs": [
1017:     {
1018:      "name": "stdout",
1019:      "output_type": "stream",
1020:      "text": [
1021:       "Total rows: 40412\n",
1022:       "Rows with HTML tags   : 203\n",
1023:       "Rows with URLs        : 109\n",
1024:       "Rows with Email IDs   : 11\n",
1025:       "{'html_tags': np.int64(203), 'urls': np.int64(109), 'emails': np.int64(11)}\n",
1026:       "Total rows: 358156\n",
1027:       "Rows with HTML tags   : 0\n",
1028:       "Rows with URLs        : 33\n",
1029:       "Rows with Email IDs   : 215\n",
1030:       "{'html_tags': np.int64(0), 'urls': np.int64(33), 'emails': np.int64(215)}\n"
1031:      ]
1032:     }
1033:    ],
1034:    "source": [
1035:     "print(count_patterns(amazon_df, \"review\"))\n",
1036:     "print(count_patterns(yelp_df, \"review\"))"
1037:    ]
1038:   },
1039:   {
1040:    "cell_type": "code",
1041:    "execution_count": 528,
1042:    "id": "7944a5ba",
1043:    "metadata": {},
1044:    "outputs": [],
1045:    "source": [
1046:     "import html\n",
1047:     "\n",
1048:     "def clean_review(text):\n",
1049:     "    # Convert to string\n",
1050:     "    text = str(text)\n",
1051:     "\n",
1052:     "    # Decode HTML entities\n",
1053:     "    text = html.unescape(text)\n",
1054:     "\n",
1055:     "    # Remove HTML tags\n",
1056:     "    text = re.sub(r\"<.*?>\", \" \", text)\n",
1057:     "\n",
1058:     "    # Remove URLs\n",
1059:     "    text = re.sub(r\"http\\\\S+|www\\\\.\\\\S+\", \" \", text)\n",
1060:     "\n",
1061:     "    # Remove email addresses\n",
1062:     "    text = re.sub(r\"\\\\S+@\\\\S+\", \" \", text)\n",
1063:     "\n",
1064:     "    # Fix common encoding artifacts\n",
1065:     "    text = re.sub(r\"[ÂâÃ]+\", \" \", text)\n",
1066:     "    \n",
1067:     "    # Remove all remaining non-ASCII characters (optional)\n",
1068:     "    text = re.sub(r\"[^\\x00-\\x7F]+\", \" \", text)\n",
1069:     "    \n",
1070:     "    # Remove extra spaces/newlines/tabs\n",
1071:     "    text = re.sub(r\"\\\\s+\", \" \", text).strip()\n",
1072:     "    \n",
1073:     "    # Remove newline, tab, and extra whitespace\n",
1074:     "    text = re.sub(r\"\\s+\", \" \", text).strip()\n",
1075:     "\n",
1076:     "    # Remove special symbols/punctuation and replace with a space\n",
1077:     "    text = re.sub(r\"[^\\w\\s]\", \" \", text)\n",
1078:     "\n",
1079:     "    # Collapse multiple spaces created after removing symbols\n",
1080:     "    text = re.sub(r\"\\s+\", \" \", text).strip()\n",
1081:     "    \n",
1082:     "    # Lowercase only\n",
1083:     "    text = text.lower()\n",
1084:     "\n",
1085:     "    return text"
1086:    ]
1087:   },
1088:   {
1089:    "cell_type": "code",
1090:    "execution_count": 529,
1091:    "id": "3f8701e8",
1092:    "metadata": {},
1093:    "outputs": [],
1094:    "source": [
1095:     "amazon_df[\"review\"] = amazon_df[\"review\"].apply(clean_review)"
1096:    ]
1097:   },
1098:   {
1099:    "cell_type": "code",
1100:    "execution_count": 530,
1101:    "id": "6bd5c901",
1102:    "metadata": {},
1103:    "outputs": [],
1104:    "source": [
1105:     "yelp_df[\"review\"] = yelp_df[\"review\"].apply(clean_review)"
1106:    ]
1107:   },
1108:   {
1109:    "cell_type": "code",
1110:    "execution_count": 531,
1111:    "id": "d0355a58",
1112:    "metadata": {},
1113:    "outputs": [
1114:     {
1115:      "name": "stdout",
1116:      "output_type": "stream",
1117:      "text": [
1118:       "Dataset Shape: (40411, 3)\n"
1119:      ]
1120:     }
1121:    ],
1122:    "source": [
1123:     "amazon_df = amazon_df[amazon_df[\"review\"].str.len() > 0].reset_index(drop=True)\n",
1124:     "\n",
1125:     "print(\"Dataset Shape:\", amazon_df.shape)"
1126:    ]
1127:   },
1128:   {
1129:    "cell_type": "code",
1130:    "execution_count": 532,
1131:    "id": "b3467bac",
1132:    "metadata": {},
1133:    "outputs": [
1134:     {
1135:      "name": "stdout",
1136:      "output_type": "stream",
1137:      "text": [
1138:       "Dataset Shape: (358142, 3)\n"
1139:      ]
1140:     }
1141:    ],
1142:    "source": [
1143:     "yelp_df = yelp_df[yelp_df[\"review\"].str.len() > 0].reset_index(drop=True)\n",
1144:     "\n",
1145:     "print(\"Dataset Shape:\", yelp_df.shape)"
1146:    ]
1147:   },
1148:   {
1149:    "cell_type": "markdown",
1150:    "id": "20bcd797",
1151:    "metadata": {},
1152:    "source": [
1153:     "### Class Distribution"
1154:    ]
1155:   },
1156:   {
1157:    "cell_type": "code",
1158:    "execution_count": 533,
1159:    "id": "1977cd89",
1160:    "metadata": {},
1161:    "outputs": [
1162:     {
1163:      "name": "stdout",
1164:      "output_type": "stream",
1165:      "text": [
1166:       "label\n",
1167:       "0    20215\n",
1168:       "1    20196\n",
1169:       "Name: count, dtype: int64\n",
1170:       "\n",
1171:       "Percentage Distribution:\n",
1172:       "label\n",
1173:       "0    50.02\n",
1174:       "1    49.98\n",
1175:       "Name: count, dtype: float64\n"
1176:      ]
1177:     }
1178:    ],
1179:    "source": [
1180:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
1181:     "\n",
1182:     "print(label_counts)\n",
1183:     "\n",
1184:     "print(\"\\nPercentage Distribution:\")\n",
1185:     "print((label_counts / len(amazon_df) * 100).round(2))"
1186:    ]
1187:   },
1188:   {
1189:    "cell_type": "code",
1190:    "execution_count": 534,
1191:    "id": "99f464ee",
1192:    "metadata": {},
1193:    "outputs": [
1194:     {
1195:      "data": {
1196:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAlsAAAH3CAYAAACM85p5AAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAXDZJREFUeJzt3Xd8k9XiBvAnSfce0EGhQBlllV32hqLsUaaCIEPR68Wr13VFvV7HVa8I4k9FRRAQERGloLJlCbRAoczSskdLBx10t2mT9/dHbCR0kLRNT97k+X4+/UDTjCdp2jw957wnCkmSJBARERGRWShFByAiIiKyZixbRERERGbEskVERERkRixbRERERGbEskVERERkRixbRERERGbEskVERERkRixbRERERGbEsmVGFy9exKZNm1BaWirs9s6fP49NmzahPveure/7XRu3bt3Cjh07sGnTJty5c0d0HKojGo0GmzZtQkJCgugoZpGcnIxNmzYhJydHdBSjlZSUYNOmTcjIyBAdhWTqwoUL2LVrl+gYNWInOoBcXL9+HbGxsfrPHR0d4eXlhdatW8Pf37/Sy2zduhUvvvgisrOz4eXlZfRtJSQk4Ny5c5gwYQJUKpXRl6vs9r7//nu8++67KC0thZ1d3X27q8tY0/td35YsWYJFixZh4MCBcHNzQ9u2bdGwYcMK5yv/3vfv37/S73VsbCyuX79u8veLKrr/5+xe/v7+6N+/v1HXU1RUhMmTJ+Ptt9/Ga6+9VpcR9c6fP48LFy7oP7e3t0dAQAA6d+4MR0dHs9xmuejoaEyePBlxcXHo3LmzWW+rrixZsgRffvklLl68WOnX8/PzsWPHDri4uGDkyJH1nM6ypaen4+DBg/rP7e3t4enpiRYtWqBJkya1uu6bN2/i2LFjGD58ODw8PGobtdaqyyNJEkaOHIk//vgDvXv3FpSwZli2jLRnzx7Mnz8f/fr1g7+/P8rKypCRkYFTp04hODgYCxcuxJNPPgmFQqG/TGhoKCIjI+Hg4GDSbW3atAmvv/468vLy4ObmZvTlanp7NVFdxvrMUVMFBQVYtGgRXnnlFfz73/+u9rzl3/vt27fj4YcfrvD1Tz/9FGvWrDH5+0UV3f9zdq+OHTsaXbbqQ/kfMsOHD4e7uzsKCwtx4sQJaDQafP7555gyZYrZbrtx48aIjIy06D9m7pWRkYH33nsPixcvrvL3wrp16/DUU08B0P0xFxoaWp8RLdqZM2cwefJkdOnSBSEhIdBqtcjKysLp06fh4eGBBQsW4J///GeNfucePHgQM2fOxNmzZ9GhQwczpK+7PO3atcOkSZPwz3/+E0eOHBGUsGZYtky0aNEigxfcoqIifPLJJ3jmmWewb98+fP/991AqdbOzY8aMwZgxY+otW33fnqXnqM61a9dQXFzMX+gW6v6fM0u2bNkytGnTBoBudGbYsGGYMWMGwsPD0bx5c7PcZq9evbBp0yazXLc5rFy5EhqNBtOnT6/yPF9//TX69euHs2fP4uuvv8aHH35Yjwnl4YknnsCCBQv0n5eVlWHNmjVYuHAhtm3bht27d8PJyUlgQvObM2cOHnroIRw7dgw9evQQHcdoLFu15OzsjJdffhnFxcV48803MWbMGMyYMQOAbu3SmTNnMG7cONjb2+svU1xcjNOnTyMjIwPNmjVDmzZt9NNPJ06cwPnz5wEAUVFR+h+coUOHwtvbWz91ERkZidLSUsTExCAnJwdjxoyp8vbKFRUV4ciRI9BqtejVqxfc3d0Nvh4bG4vU1FSMHj3a4PT7h3UflLG6HFlZWThx4gTUajXatm2LkJAQg6/ff/8OHz4MtVqNXr16wdPT0+jvS3W3ExMTg3379unvs52dHTw8PDB8+HCjr/9BjH0sAcP7XFJSgiNHjkClUqFv3776qd/i4mJER0ejrKwM/fr1g7Ozc6XXCwAKhQKurq7o0KEDGjdubHC+2jy+8fHx... (line truncated to 2000 chars)
1197:       "text/plain": [
1198:        "<Figure size 600x600 with 1 Axes>"
1199:       ]
1200:      },
1201:      "metadata": {},
1202:      "output_type": "display_data"
1203:     }
1204:    ],
1205:    "source": [
1206:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
1207:     "\n",
1208:     "# Pie chart\n",
1209:     "plt.figure(figsize=(6, 6))\n",
1210:     "\n",
1211:     "plt.pie(\n",
1212:     "    label_counts,\n",
1213:     "    labels=[\"Human (0)\", \"CG (1)\"],\n",
1214:     "    autopct=\"%1.1f%%\",\n",
1215:     "    startangle=90\n",
1216:     ")\n",
1217:     "\n",
1218:     "plt.title(\"Distribution of Human vs Fake Reviews (Amazon Dataset)\")\n",
1219:     "plt.axis(\"equal\")\n",
1220:     "\n",
1221:     "plt.show()"
1222:    ]
1223:   },
1224:   {
1225:    "cell_type": "code",
1226:    "execution_count": 535,
1227:    "id": "c83f6a6e",
1228:    "metadata": {},
1229:    "outputs": [
1230:     {
1231:      "name": "stdout",
1232:      "output_type": "stream",
1233:      "text": [
1234:       "label\n",
1235:       "0    321568\n",
1236:       "1     36574\n",
1237:       "Name: count, dtype: int64\n",
1238:       "\n",
1239:       "Percentage Distribution:\n",
1240:       "label\n",
1241:       "0    89.79\n",
1242:       "1    10.21\n",
1243:       "Name: count, dtype: float64\n"
1244:      ]
1245:     }
1246:    ],
1247:    "source": [
1248:     "label_counts = yelp_df[\"label\"].value_counts().sort_index()\n",
1249:     "\n",
1250:     "print(label_counts)\n",
1251:     "\n",
1252:     "print(\"\\nPercentage Distribution:\")\n",
1253:     "print((label_counts / len(yelp_df) * 100).round(2))"
1254:    ]
1255:   },
1256:   {
1257:    "cell_type": "code",
1258:    "execution_count": 536,
1259:    "id": "9ba9dd68",
1260:    "metadata": {},
1261:    "outputs": [
1262:     {
1263:      "data": {
1264:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAf0AAAH3CAYAAACxV4buAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAYgVJREFUeJzt3Xd4VGXCBfAzk947IaQASSB0CR0p0gJSVCDCUkQFEdQVRdRdy+7qt/ay2BVEwAaidKT3EggtBEINpDdCei+TzLzfHzEDIYX0d8r5PU8eyOTOvWcmkzlz39sUQggBIiIiMnhK2QGIiIiodbD0iYiIjARLn4iIyEiw9ImIiIwES5+IiMhIsPSJiIiMBEufiIjISLD0iYiIjESLl35cXBw2bNiAoqKill5Urcu7fv06NmzYAJVK1SoZasuhq27evIm9e/diw4YNSElJkR2HmtGmTZtw8eJF2TFaRFpaGjZs2ID09HTZUepNrVZj48aNuHnzpuwopKeioqKwY8eORt/ftCETJycnIzQ0VPu9ubk5HBwc0KlTJ7Rr167G++zfvx9PP/00YmNj0aFDh3ovKzo6GuHh4Zg4cSKsrKzqfb+alrdt2za8+uqrSE9Ph6ura73n1ZSMjX3cre2HH37AokWLMHToUDg4OKB9+/Y1/i4rf/eDBg2Cl5dXtZ9fuHABN27caPDvi6q7++/sTs7Ozhg1alS95zV9+nQsXrwYn376aXPFq+L69euIiIjQfm9qaoo2bdogMDCwxV8HERERmDZtGg4dOoQRI0a06LKay/fff4+33noLMTExNf5cpVJh27ZtMDU1xeTJk1s3nI7Lzs7GgQMHtN+bmZnB3t4eHTt2bPJ7bGpqKkJCQjBy5Ei4uLg0MWnT1ZXH3NwcU6dOxdatW/Hggw82fOaiAdavXy8AiIEDB4rg4GAxefJkMWzYMGFvby/8/f3F0qVLRXl5eZX77N+/XwQHB4u0tLSGLEp89dVXAoBITExs0P1qWt4nn3wiAIj09PQGzaspGRv7uFuTWq0WDg4OYvHixfectvJ3/9tvv9X48xdffLFRvy+q7u6/szu//vGPfzRoXiYmJuLll19uoaS3/7ZGjhwpgoODxcSJE0W7du2Eg4ODWLlyZYstVwghIiIiRHBwsLh06VKLLqe55OfnCzc3N/HRRx/VOs1vv/0mAAgA4uTJk62YTvedOXNGABA9evQQwcHBYsqUKWLkyJHCxcVFtGvXTvznP/8RRUVFjZr3n3/+KQCIY8eONXPqxrlXnoULF4ru3bsLjUbT4Hk3aE2/0uLFizFjxgzt9yqVCsuXL8crr7yCvXv34s8//4SpacWsR48ejdGjRzdmMY3S2svT9Rx1SUlJQW5uLgICAmRHoRrc/Xemy95//30MGjQIAFBSUoJJkyZh/vz56NevH3r16tUiy+zZsyc2bNjQIvNuCWvWrEF2djaeeOKJWqf54Ycf0KdPH9y8eRM//PADBg4c2IoJ9cPs2bPx2muvab/XaDRYt24dnnvuOfz55584cuQI7OzsJCZsefPmzcPy5cuxb98+jB07tkH3bVTp383c3ByLFi2CRqPB4sWLsWzZMjz//PMAKrZtnz17FhMmTIC1tbX2PmVlZTh//jzS0tLg7e2Nrl27wszMDABw8eJFnD9/HgCwc+dOODs7AwCGDx+ONm3aaIcUH374YSiVSpw8eRLp6emYMmVKrcurpFKpcOLECZSUlGDQoEFwdHSs8vMLFy4gJiYGU6ZMqXL73cMt98pYV47c3FycPXsWxcXF6Ny5Mzp37lzl53c/vhMnTqCwsBADBgxo0NBTXcsJCwvD8ePHtY95w4YNsLS0xKRJk+o9/3up73MJVH3MAHDixAkIIXD//ffDwsICQMXvLjQ0FCUlJRgyZAhsbW1rnC8AKBQKWFtbo2vXrtWG/pry/EZFReH8+fMICgqCg4NDlZ8VFRVh586d6NGjB7p06QKg... (line truncated to 2000 chars)
1265:       "text/plain": [
1266:        "<Figure size 600x600 with 1 Axes>"
1267:       ]
1268:      },
1269:      "metadata": {},
1270:      "output_type": "display_data"
1271:     }
1272:    ],
1273:    "source": [
1274:     "label_counts = yelp_df[\"label\"].value_counts().sort_index()\n",
1275:     "\n",
1276:     "# Pie chart\n",
1277:     "plt.figure(figsize=(6, 6))\n",
1278:     "\n",
1279:     "plt.pie(\n",
1280:     "    label_counts,\n",
1281:     "    labels=[\"Human (0)\", \"CG (1)\"],\n",
1282:     "    autopct=\"%1.1f%%\",\n",
1283:     "    startangle=90\n",
1284:     ")\n",
1285:     "\n",
1286:     "plt.title(\"Distribution of Human vs Fake Reviews (Amazon Dataset)\")\n",
1287:     "plt.axis(\"equal\")\n",
1288:     "\n",
1289:     "plt.show()"
1290:    ]
1291:   },
1292:   {
1293:    "cell_type": "markdown",
1294:    "id": "55ffc64d",
1295:    "metadata": {},
1296:    "source": [
1297:     "#### Balance Yelp Dataset\n"
1298:    ]
1299:   },
1300:   {
1301:    "cell_type": "markdown",
1302:    "id": "87109c19",
1303:    "metadata": {},
1304:    "source": [
1305:     "randomly sample 25k from each class to create a balanced subset, since the original Yelp data is heavily skewed (~90% genuine)"
1306:    ]
1307:   },
1308:   {
1309:    "cell_type": "code",
1310:    "execution_count": 537,
1311:    "id": "3bdf9942",
1312:    "metadata": {},
1313:    "outputs": [
1314:     {
1315:      "name": "stdout",
1316:      "output_type": "stream",
1317:      "text": [
1318:       "Label counts:\n",
1319:       " label\n",
1320:       "1    25000\n",
1321:       "0    25000\n",
1322:       "Name: count, dtype: int64\n"
1323:      ]
1324:     }
1325:    ],
1326:    "source": [
1327:     "fake = yelp_df[yelp_df['label'] == 0].sample(n=25000, random_state=42)\n",
1328:     "real = yelp_df[yelp_df['label'] == 1].sample(n=25000, random_state=42)\n",
1329:     "\n",
1330:     "yelp_sample = (\n",
1331:     "    pd.concat([fake, real])\n",
1332:     "      .sample(frac=1, random_state=42)   # shuffle\n",
1333:     "      .reset_index(drop=True)\n",
1334:     ")\n",
1335:     "print(\"Label counts:\\n\", yelp_sample['label'].value_counts())"
1336:    ]
1337:   },
1338:   {
1339:    "cell_type": "code",
1340:    "execution_count": 538,
1341:    "id": "f29b9a60",
1342:    "metadata": {},
1343:    "outputs": [
1344:     {
1345:      "name": "stdout",
1346:      "output_type": "stream",
1347:      "text": [
1348:       "Label counts:\n",
1349:       " label\n",
1350:       "0    20215\n",
1351:       "1    20196\n",
1352:       "Name: count, dtype: int64\n"
1353:      ]
1354:     }
1355:    ],
1356:    "source": [
1357:     "print(\"Label counts:\\n\", amazon_df['label'].value_counts())"
1358:    ]
1359:   },
1360:   {
1361:    "cell_type": "markdown",
1362:    "id": "69cc9285",
1363:    "metadata": {},
1364:    "source": [
1365:     "### Review Length Filtering"
1366:    ]
1367:   },
1368:   {
1369:    "cell_type": "code",
1370:    "execution_count": 539,
1371:    "id": "1c3c0c8d",
1372:    "metadata": {},
1373:    "outputs": [
1374:     {
1375:      "name": "stdout",
1376:      "output_type": "stream",
1377:      "text": [
1378:       "Empty Reviews : 0\n",
1379:       "Average Review Length : 339.90292247160426\n",
1380:       "Shortest Review Length : 4\n",
1381:       "Longest Review Length : 2095\n"
1382:      ]
1383:     }
1384:    ],
1385:    "source": [
1386:     "#amazon\n",
1387:     "\n",
1388:     "print(\"Empty Reviews :\", (amazon_df[\"review\"] == \"\").sum())\n",
1389:     "\n",
1390:     "print(\"Average Review Length :\", amazon_df[\"review\"].str.len().mean())\n",
1391:     "\n",
1392:     "print(\"Shortest Review Length :\", amazon_df[\"review\"].str.len().min())\n",
1393:     "\n",
1394:     "print(\"Longest Review Length :\", amazon_df[\"review\"].str.len().max())"
1395:    ]
1396:   },
1397:   {
1398:    "cell_type": "code",
1399:    "execution_count": 540,
1400:    "id": "f5bf54a4",
1401:    "metadata": {},
1402:    "outputs": [
1403:     {
1404:      "data": {
1405:       "text/html": [
1406:        "<div>\n",
1407:        "<style scoped>\n",
1408:        "    .dataframe tbody tr th:only-of-type {\n",
1409:        "        vertical-align: middle;\n",
1410:        "    }\n",
1411:        "\n",
1412:        "    .dataframe tbody tr th {\n",
1413:        "        vertical-align: top;\n",
1414:        "    }\n",
1415:        "\n",
1416:        "    .dataframe thead th {\n",
1417:        "        text-align: right;\n",
1418:        "    }\n",
1419:        "</style>\n",
1420:        "<table border=\"1\" class=\"dataframe\">\n",
1421:        "  <thead>\n",
1422:        "    <tr style=\"text-align: right;\">\n",
1423:        "      <th></th>\n",
1424:        "      <th>rating</th>\n",
1425:        "      <th>review</th>\n",
1426:        "      <th>label</th>\n",
1427:        "    </tr>\n",
1428:        "  </thead>\n",
1429:        "  <tbody>\n",
1430:        "    <tr>\n",
1431:        "      <th>9907</th>\n",
1432:        "      <td>5</td>\n",
1433:        "      <td>input</td>\n",
1434:        "      <td>1</td>\n",
1435:        "    </tr>\n",
1436:        "    <tr>\n",
1437:        "      <th>18615</th>\n",
1438:        "      <td>3</td>\n",
1439:        "      <td>pfister lf 042 prcc</td>\n",
1440:        "      <td>1</td>\n",
1441:        "    </tr>\n",
1442:        "    <tr>\n",
1443:        "      <th>21677</th>\n",
1444:        "      <td>5</td>\n",
1445:        "      <td>well</td>\n",
1446:        "      <td>1</td>\n",
1447:        "    </tr>\n",
1448:        "    <tr>\n",
1449:        "      <th>36815</th>\n",
1450:        "      <td>5</td>\n",
1451:        "      <td>nice elegant watch</td>\n",
1452:        "      <td>1</td>\n",
1453:        "    </tr>\n",
1454:        "  </tbody>\n",
1455:        "</table>\n",
1456:        "</div>"
1457:       ],
1458:       "text/plain": [
1459:        "       rating               review  label\n",
1460:        "9907        5                input      1\n",
1461:        "18615       3  pfister lf 042 prcc      1\n",
1462:        "21677       5                 well      1\n",
1463:        "36815       5   nice elegant watch      1"
1464:       ]
1465:      },
1466:      "execution_count": 540,
1467:      "metadata": {},
1468:      "output_type": "execute_result"
1469:     }
1470:    ],
1471:    "source": [
1472:     "# Print rows where text has fewer than 20 characters\n",
1473:     "amazon_df[amazon_df[\"review\"].str.len() < 20]"
1474:    ]
1475:   },
1476:   {
1477:    "cell_type": "code",
1478:    "execution_count": 541,
1479:    "id": "6f0277ef",
1480:    "metadata": {},
1481:    "outputs": [
1482:     {
1483:      "data": {
1484:       "text/html": [
1485:        "<div>\n",
1486:        "<style scoped>\n",
1487:        "    .dataframe tbody tr th:only-of-type {\n",
1488:        "        vertical-align: middle;\n",
1489:        "    }\n",
1490:        "\n",
1491:        "    .dataframe tbody tr th {\n",
1492:        "        vertical-align: top;\n",
1493:        "    }\n",
1494:        "\n",
1495:        "    .dataframe thead th {\n",
1496:        "        text-align: right;\n",
1497:        "    }\n",
1498:        "</style>\n",
1499:        "<table border=\"1\" class=\"dataframe\">\n",
1500:        "  <thead>\n",
1501:        "    <tr style=\"text-align: right;\">\n",
1502:        "      <th></th>\n",
1503:        "      <th>rating</th>\n",
1504:        "      <th>review</th>\n",
1505:        "      <th>label</th>\n",
1506:        "    </tr>\n",
1507:        "  </thead>\n",
1508:        "  <tbody>\n",
1509:        "    <tr>\n",
1510:        "      <th>2410</th>\n",
1511:        "      <td>1</td>\n",
1512:        "      <td>i had a hard time contacting the manufacturer distributor in order to make sure the measurements were correct the description and the pdf have completely different dimensions in reality these didn...</td>\n",

(Output capped at 50 KB. Showing lines 1-1512. Use offset=1513 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 3.0s)

_Thinking:_

Let me continue reading to see the rest of the notebook.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 1513
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
1513:        "      <td>0</td>\n",
1514:        "    </tr>\n",
1515:        "    <tr>\n",
1516:        "      <th>2578</th>\n",
1517:        "      <td>5</td>\n",
1518:        "      <td>i purchased this bed and have slept on it for the past week i believe in trying things out to make sure my guests won t suffer from backaches etc the aerobed provides a comfortable night s rest i ...</td>\n",
1519:        "      <td>0</td>\n",
1520:        "    </tr>\n",
1521:        "    <tr>\n",
1522:        "      <th>2605</th>\n",
1523:        "      <td>4</td>\n",
1524:        "      <td>after my first night sleeping on a neckbone pillow i ordered another one so my husband could have his own too i could already feel improvement in my neck and shoulder problems after just one night...</td>\n",
1525:        "      <td>0</td>\n",
1526:        "    </tr>\n",
1527:        "    <tr>\n",
1528:        "      <th>2608</th>\n",
1529:        "      <td>5</td>\n",
1530:        "      <td>these canisters are the perfect size for us we use the smallest one for powdered creamer the middle size for instant coffee and the largest size for sugar which we use to refill our smaller sugar ...</td>\n",
1531:        "      <td>0</td>\n",
1532:        "    </tr>\n",
1533:        "    <tr>\n",
1534:        "      <th>2637</th>\n",
1535:        "      <td>5</td>\n",
1536:        "      <td>these are really wonderful they are perfect for strawberry hulling neatly and easily i ve owned a dozen not because they wear out they don t they just seem to wander away when i m not looking fort...</td>\n",
1537:        "      <td>0</td>\n",
1538:        "    </tr>\n",
1539:        "    <tr>\n",
1540:        "      <th>...</th>\n",
1541:        "      <td>...</td>\n",
1542:        "      <td>...</td>\n",
1543:        "      <td>...</td>\n",
1544:        "    </tr>\n",
1545:        "    <tr>\n",
1546:        "      <th>40406</th>\n",
1547:        "      <td>4</td>\n",
1548:        "      <td>i had read some reviews saying that this bra ran small and so i ordered two band and cup sizes up and it was still too small definitely along the lines of a sports bra squish effect the sides do c...</td>\n",
1549:        "      <td>0</td>\n",
1550:        "    </tr>\n",
1551:        "    <tr>\n",
1552:        "      <th>40407</th>\n",
1553:        "      <td>5</td>\n",
1554:        "      <td>i wasn t sure exactly what it would be it is a little large for my small size but i think it is a nice fit the fabric is a nice thin material but it is a little thin in the legs i wish it was thic...</td>\n",
1555:        "      <td>1</td>\n",
1556:        "    </tr>\n",
1557:        "    <tr>\n",
1558:        "      <th>40408</th>\n",
1559:        "      <td>2</td>\n",
1560:        "      <td>you can wear the hood by itself wear it with the hood or wear just the jacket without the hood how is that for 3 in 1 systems reminiscent of what lands end sells as a squall jacket or what uniform...</td>\n",
1561:        "      <td>0</td>\n",
1562:        "    </tr>\n",
1563:        "    <tr>\n",
1564:        "      <th>40409</th>\n",
1565:        "      <td>1</td>\n",
1566:        "      <td>i liked nothing about this dress the only reason i gave it 4 stars is because i ordered the size 6 5 and it fit perfectly the fabric is a nice thin material and the color is vibrant it s a little ...</td>\n",
1567:        "      <td>1</td>\n",
1568:        "    </tr>\n",
1569:        "    <tr>\n",
1570:        "      <th>40410</th>\n",
1571:        "      <td>5</td>\n",
1572:        "      <td>i work in the wedding industry and have to work long days on my feet outside in the heat and have to look professional i ve spent a ridiculous amount of money on high end dress shoes like merrels ...</td>\n",
1573:        "      <td>0</td>\n",
1574:        "    </tr>\n",
1575:        "  </tbody>\n",
1576:        "</table>\n",
1577:        "<p>14050 rows × 3 columns</p>\n",
1578:        "</div>"
1579:       ],
1580:       "text/plain": [
1581:        "       rating  \\\n",
1582:        "2410        1   \n",
1583:        "2578        5   \n",
1584:        "2605        4   \n",
1585:        "2608        5   \n",
1586:        "2637        5   \n",
1587:        "...       ...   \n",
1588:        "40406       4   \n",
1589:        "40407       5   \n",
1590:        "40408       2   \n",
1591:        "40409       1   \n",
1592:        "40410       5   \n",
1593:        "\n",
1594:        "                                                                                                                                                                                                        review  \\\n",
1595:        "2410   i had a hard time contacting the manufacturer distributor in order to make sure the measurements were correct the description and the pdf have completely different dimensions in reality these didn...   \n",
1596:        "2578   i purchased this bed and have slept on it for the past week i believe in trying things out to make sure my guests won t suffer from backaches etc the aerobed provides a comfortable night s rest i ...   \n",
1597:        "2605   after my first night sleeping on a neckbone pillow i ordered another one so my husband could have his own too i could already feel improvement in my neck and shoulder problems after just one night...   \n",
1598:        "2608   these canisters are the perfect size for us we use the smallest one for powdered creamer the middle size for instant coffee and the largest size for sugar which we use to refill our smaller sugar ...   \n",
1599:        "2637   these are really wonderful they are perfect for strawberry hulling neatly and easily i ve owned a dozen not because they wear out they don t they just seem to wander away when i m not looking fort...   \n",
1600:        "...                                                                                                                                                                                                        ...   \n",
1601:        "40406  i had read some reviews saying that this bra ran small and so i ordered two band and cup sizes up and it was still too small definitely along the lines of a sports bra squish effect the sides do c...   \n",
1602:        "40407  i wasn t sure exactly what it would be it is a little large for my small size but i think it is a nice fit the fabric is a nice thin material but it is a little thin in the legs i wish it was thic...   \n",
1603:        "40408  you can wear the hood by itself wear it with the hood or wear just the jacket without the hood how is that for 3 in 1 systems reminiscent of what lands end sells as a squall jacket or what uniform...   \n",
1604:        "40409  i liked nothing about this dress the only reason i gave it 4 stars is because i ordered the size 6 5 and it fit perfectly the fabric is a nice thin material and the color is vibrant it s a little ...   \n",
1605:        "40410  i work in the wedding industry and have to work long days on my feet outside in the heat and have to look professional i ve spent a ridiculous amount of money on high end dress shoes like merrels ...   \n",
1606:        "\n",
1607:        "       label  \n",
1608:        "2410       0  \n",
1609:        "2578       0  \n",
1610:        "2605       0  \n",
1611:        "2608       0  \n",
1612:        "2637       0  \n",
1613:        "...      ...  \n",
1614:        "40406      0  \n",
1615:        "40407      1  \n",
1616:        "40408      0  \n",
1617:        "40409      1  \n",
1618:        "40410      0  \n",
1619:        "\n",
1620:        "[14050 rows x 3 columns]"
1621:       ]
1622:      },
1623:      "execution_count": 541,
1624:      "metadata": {},
1625:      "output_type": "execute_result"
1626:     }
1627:    ],
1628:    "source": [
1629:     "amazon_df[amazon_df[\"review\"].str.len() > 300]"
1630:    ]
1631:   },
1632:   {
1633:    "cell_type": "code",
1634:    "execution_count": 542,
1635:    "id": "37ef9503",
1636:    "metadata": {},
1637:    "outputs": [
1638:     {
1639:      "name": "stdout",
1640:      "output_type": "stream",
1641:      "text": [
1642:       "Label Distribution (Count):\n",
1643:       "label\n",
1644:       "0    7819\n",
1645:       "1    6231\n",
1646:       "Name: count, dtype: int64\n",
1647:       "\n",
1648:       "Label Distribution (Percentage):\n",
1649:       "label\n",
1650:       "0    55.65\n",
1651:       "1    44.35\n",
1652:       "Name: count, dtype: float64\n"
1653:      ]
1654:     }
1655:    ],
1656:    "source": [
1657:     "long_reviews = amazon_df[amazon_df[\"review\"].str.len() >300]\n",
1658:     "\n",
1659:     "# Label counts\n",
1660:     "label_counts = long_reviews[\"label\"].value_counts().sort_index()\n",
1661:     "\n",
1662:     "print(\"Label Distribution (Count):\")\n",
1663:     "print(label_counts)\n",
1664:     "\n",
1665:     "print(\"\\nLabel Distribution (Percentage):\")\n",
1666:     "print((label_counts / len(long_reviews) * 100).round(2))"
1667:    ]
1668:   },
1669:   {
1670:    "cell_type": "code",
1671:    "execution_count": 543,
1672:    "id": "395aa86d",
1673:    "metadata": {},
1674:    "outputs": [
1675:     {
1676:      "name": "stdout",
1677:      "output_type": "stream",
1678:      "text": [
1679:       "Empty Reviews : 0\n",
1680:       "Average Review Length : 529.96384\n",
1681:       "Shortest Review Length : 1\n",
1682:       "Longest Review Length : 4907\n"
1683:      ]
1684:     }
1685:    ],
1686:    "source": [
1687:     "#yelp\n",
1688:     "\n",
1689:     "print(\"Empty Reviews :\", (yelp_sample[\"review\"] == \"\").sum())\n",
1690:     "\n",
1691:     "print(\"Average Review Length :\", yelp_sample[\"review\"].str.len().mean())\n",
1692:     "\n",
1693:     "print(\"Shortest Review Length :\", yelp_sample[\"review\"].str.len().min())\n",
1694:     "\n",
1695:     "print(\"Longest Review Length :\", yelp_sample[\"review\"].str.len().max())"
1696:    ]
1697:   },
1698:   {
1699:    "cell_type": "code",
1700:    "execution_count": 544,
1701:    "id": "02f9e6a4",
1702:    "metadata": {},
1703:    "outputs": [
1704:     {
1705:      "data": {
1706:       "text/html": [
1707:        "<div>\n",
1708:        "<style scoped>\n",
1709:        "    .dataframe tbody tr th:only-of-type {\n",
1710:        "        vertical-align: middle;\n",
1711:        "    }\n",
1712:        "\n",
1713:        "    .dataframe tbody tr th {\n",
1714:        "        vertical-align: top;\n",
1715:        "    }\n",
1716:        "\n",
1717:        "    .dataframe thead th {\n",
1718:        "        text-align: right;\n",
1719:        "    }\n",
1720:        "</style>\n",
1721:        "<table border=\"1\" class=\"dataframe\">\n",
1722:        "  <thead>\n",
1723:        "    <tr style=\"text-align: right;\">\n",
1724:        "      <th></th>\n",
1725:        "      <th>rating</th>\n",
1726:        "      <th>review</th>\n",
1727:        "      <th>label</th>\n",
1728:        "    </tr>\n",
1729:        "  </thead>\n",
1730:        "  <tbody>\n",
1731:        "    <tr>\n",
1732:        "      <th>56</th>\n",
1733:        "      <td>5</td>\n",
1734:        "      <td>still the best</td>\n",
1735:        "      <td>1</td>\n",
1736:        "    </tr>\n",
1737:        "    <tr>\n",
1738:        "      <th>75</th>\n",
1739:        "      <td>5</td>\n",
1740:        "      <td>love this place</td>\n",
1741:        "      <td>1</td>\n",
1742:        "    </tr>\n",
1743:        "    <tr>\n",
1744:        "      <th>421</th>\n",
1745:        "      <td>5</td>\n",
1746:        "      <td>5</td>\n",
1747:        "      <td>1</td>\n",
1748:        "    </tr>\n",
1749:        "    <tr>\n",
1750:        "      <th>854</th>\n",
1751:        "      <td>5</td>\n",
1752:        "      <td>great place</td>\n",
1753:        "      <td>1</td>\n",
1754:        "    </tr>\n",
1755:        "    <tr>\n",
1756:        "      <th>908</th>\n",
1757:        "      <td>3</td>\n",
1758:        "      <td>i like the drinks</td>\n",
1759:        "      <td>1</td>\n",
1760:        "    </tr>\n",
1761:        "    <tr>\n",
1762:        "      <th>...</th>\n",
1763:        "      <td>...</td>\n",
1764:        "      <td>...</td>\n",
1765:        "      <td>...</td>\n",
1766:        "    </tr>\n",
1767:        "    <tr>\n",
1768:        "      <th>49848</th>\n",
1769:        "      <td>5</td>\n",
1770:        "      <td>excellent</td>\n",
1771:        "      <td>1</td>\n",
1772:        "    </tr>\n",
1773:        "    <tr>\n",
1774:        "      <th>49858</th>\n",
1775:        "      <td>5</td>\n",
1776:        "      <td>love it</td>\n",
1777:        "      <td>0</td>\n",
1778:        "    </tr>\n",
1779:        "    <tr>\n",
1780:        "      <th>49877</th>\n",
1781:        "      <td>5</td>\n",
1782:        "      <td>yum</td>\n",
1783:        "      <td>1</td>\n",
1784:        "    </tr>\n",
1785:        "    <tr>\n",
1786:        "      <th>49961</th>\n",
1787:        "      <td>4</td>\n",
1788:        "      <td>nom</td>\n",
1789:        "      <td>1</td>\n",
1790:        "    </tr>\n",
1791:        "    <tr>\n",
1792:        "      <th>49996</th>\n",
1793:        "      <td>5</td>\n",
1794:        "      <td>looks good</td>\n",
1795:        "      <td>1</td>\n",
1796:        "    </tr>\n",
1797:        "  </tbody>\n",
1798:        "</table>\n",
1799:        "<p>570 rows × 3 columns</p>\n",
1800:        "</div>"
1801:       ],
1802:       "text/plain": [
1803:        "       rating             review  label\n",
1804:        "56          5     still the best      1\n",
1805:        "75          5    love this place      1\n",
1806:        "421         5                  5      1\n",
1807:        "854         5        great place      1\n",
1808:        "908         3  i like the drinks      1\n",
1809:        "...       ...                ...    ...\n",
1810:        "49848       5          excellent      1\n",
1811:        "49858       5            love it      0\n",
1812:        "49877       5                yum      1\n",
1813:        "49961       4                nom      1\n",
1814:        "49996       5         looks good      1\n",
1815:        "\n",
1816:        "[570 rows x 3 columns]"
1817:       ]
1818:      },
1819:      "execution_count": 544,
1820:      "metadata": {},
1821:      "output_type": "execute_result"
1822:     }
1823:    ],
1824:    "source": [
1825:     "# Print rows where text has fewer than 20 characters\n",
1826:     "yelp_sample[yelp_sample[\"review\"].str.len() < 20]"
1827:    ]
1828:   },
1829:   {
1830:    "cell_type": "code",
1831:    "execution_count": 545,
1832:    "id": "5bf7419d",
1833:    "metadata": {},
1834:    "outputs": [
1835:     {
1836:      "name": "stdout",
1837:      "output_type": "stream",
1838:      "text": [
1839:       "Label Distribution (Count):\n",
1840:       "label\n",
1841:       "0    117\n",
1842:       "1    453\n",
1843:       "Name: count, dtype: int64\n",
1844:       "\n",
1845:       "Label Distribution (Percentage):\n",
1846:       "label\n",
1847:       "0    20.53\n",
1848:       "1    79.47\n",
1849:       "Name: count, dtype: float64\n"
1850:      ]
1851:     }
1852:    ],
1853:    "source": [
1854:     "short_yelp_reviews = yelp_sample[yelp_sample[\"review\"].str.len() < 20]\n",
1855:     "\n",
1856:     "# Label counts\n",
1857:     "label_counts = short_yelp_reviews[\"label\"].value_counts().sort_index()\n",
1858:     "\n",
1859:     "print(\"Label Distribution (Count):\")\n",
1860:     "print(label_counts)\n",
1861:     "\n",
1862:     "print(\"\\nLabel Distribution (Percentage):\")\n",
1863:     "print((label_counts / len(short_yelp_reviews) * 100).round(2))"
1864:    ]
1865:   },
1866:   {
1867:    "cell_type": "code",
1868:    "execution_count": 546,
1869:    "id": "d3a4beb9",
1870:    "metadata": {},
1871:    "outputs": [
1872:     {
1873:      "data": {
1874:       "text/html": [
1875:        "<div>\n",
1876:        "<style scoped>\n",
1877:        "    .dataframe tbody tr th:only-of-type {\n",
1878:        "        vertical-align: middle;\n",
1879:        "    }\n",
1880:        "\n",
1881:        "    .dataframe tbody tr th {\n",
1882:        "        vertical-align: top;\n",
1883:        "    }\n",
1884:        "\n",
1885:        "    .dataframe thead th {\n",
1886:        "        text-align: right;\n",
1887:        "    }\n",
1888:        "</style>\n",
1889:        "<table border=\"1\" class=\"dataframe\">\n",
1890:        "  <thead>\n",
1891:        "    <tr style=\"text-align: right;\">\n",
1892:        "      <th></th>\n",
1893:        "      <th>rating</th>\n",
1894:        "      <th>review</th>\n",
1895:        "      <th>label</th>\n",
1896:        "      <th>review_length</th>\n",
1897:        "    </tr>\n",
1898:        "  </thead>\n",
1899:        "  <tbody>\n",
1900:        "    <tr>\n",
1901:        "      <th>48267</th>\n",
1902:        "      <td>5</td>\n",
1903:        "      <td>cheap and delicious</td>\n",
1904:        "      <td>1</td>\n",
1905:        "      <td>19</td>\n",
1906:        "    </tr>\n",
1907:        "    <tr>\n",
1908:        "      <th>47366</th>\n",
1909:        "      <td>5</td>\n",
1910:        "      <td>very very very good</td>\n",
1911:        "      <td>1</td>\n",
1912:        "      <td>19</td>\n",
1913:        "    </tr>\n",
1914:        "    <tr>\n",
1915:        "      <th>45673</th>\n",
1916:        "      <td>5</td>\n",
1917:        "      <td>great place love it</td>\n",
1918:        "      <td>1</td>\n",
1919:        "      <td>19</td>\n",
1920:        "    </tr>\n",
1921:        "    <tr>\n",
1922:        "      <th>2359</th>\n",
1923:        "      <td>3</td>\n",
1924:        "      <td>white sauce is good</td>\n",
1925:        "      <td>1</td>\n",
1926:        "      <td>19</td>\n",
1927:        "    </tr>\n",
1928:        "    <tr>\n",
1929:        "      <th>3039</th>\n",
1930:        "      <td>4</td>\n",
1931:        "      <td>i loved their tacos</td>\n",
1932:        "      <td>1</td>\n",
1933:        "      <td>19</td>\n",
1934:        "    </tr>\n",
1935:        "    <tr>\n",
1936:        "      <th>...</th>\n",
1937:        "      <td>...</td>\n",
1938:        "      <td>...</td>\n",
1939:        "      <td>...</td>\n",
1940:        "      <td>...</td>\n",
1941:        "    </tr>\n",
1942:        "    <tr>\n",
1943:        "      <th>40750</th>\n",
1944:        "      <td>5</td>\n",
1945:        "      <td>yum</td>\n",
1946:        "      <td>0</td>\n",
1947:        "      <td>3</td>\n",
1948:        "    </tr>\n",
1949:        "    <tr>\n",
1950:        "      <th>49961</th>\n",
1951:        "      <td>4</td>\n",
1952:        "      <td>nom</td>\n",
1953:        "      <td>1</td>\n",
1954:        "      <td>3</td>\n",
1955:        "    </tr>\n",
1956:        "    <tr>\n",
1957:        "      <th>44802</th>\n",
1958:        "      <td>5</td>\n",
1959:        "      <td>woo</td>\n",
1960:        "      <td>1</td>\n",
1961:        "      <td>3</td>\n",
1962:        "    </tr>\n",
1963:        "    <tr>\n",
1964:        "      <th>23950</th>\n",
1965:        "      <td>2</td>\n",
1966:        "      <td>ok</td>\n",
1967:        "      <td>1</td>\n",
1968:        "      <td>2</td>\n",
1969:        "    </tr>\n",
1970:        "    <tr>\n",
1971:        "      <th>421</th>\n",
1972:        "      <td>5</td>\n",
1973:        "      <td>5</td>\n",
1974:        "      <td>1</td>\n",
1975:        "      <td>1</td>\n",
1976:        "    </tr>\n",
1977:        "  </tbody>\n",
1978:        "</table>\n",
1979:        "<p>570 rows × 4 columns</p>\n",
1980:        "</div>"
1981:       ],
1982:       "text/plain": [
1983:        "       rating               review  label  review_length\n",
1984:        "48267       5  cheap and delicious      1             19\n",
1985:        "47366       5  very very very good      1             19\n",
1986:        "45673       5  great place love it      1             19\n",
1987:        "2359        3  white sauce is good      1             19\n",
1988:        "3039        4  i loved their tacos      1             19\n",
1989:        "...       ...                  ...    ...            ...\n",
1990:        "40750       5                  yum      0              3\n",
1991:        "49961       4                  nom      1              3\n",
1992:        "44802       5                  woo      1              3\n",
1993:        "23950       2                   ok      1              2\n",
1994:        "421         5                    5      1              1\n",
1995:        "\n",
1996:        "[570 rows x 4 columns]"
1997:       ]
1998:      },
1999:      "execution_count": 546,
2000:      "metadata": {},
2001:      "output_type": "execute_result"
2002:     }
2003:    ],
2004:    "source": [
2005:     "yelp_sample[\n",
2006:     "    yelp_sample[\"review\"].str.len() < 20\n",
2007:     "].assign(\n",
2008:     "    review_length=yelp_sample[\"review\"].str.len()\n",
2009:     ").sort_values(\n",
2010:     "    by=\"review_length\", ascending=False\n",
2011:     ")"
2012:    ]
2013:   },
2014:   {
2015:    "cell_type": "code",
2016:    "execution_count": 547,
2017:    "id": "f96d07a5",
2018:    "metadata": {},
2019:    "outputs": [
2020:     {
2021:      "data": {
2022:       "text/html": [
2023:        "<div>\n",
2024:        "<style scoped>\n",
2025:        "    .dataframe tbody tr th:only-of-type {\n",
2026:        "        vertical-align: middle;\n",
2027:        "    }\n",
2028:        "\n",
2029:        "    .dataframe tbody tr th {\n",
2030:        "        vertical-align: top;\n",
2031:        "    }\n",
2032:        "\n",
2033:        "    .dataframe thead th {\n",
2034:        "        text-align: right;\n",
2035:        "    }\n",
2036:        "</style>\n",
2037:        "<table border=\"1\" class=\"dataframe\">\n",
2038:        "  <thead>\n",
2039:        "    <tr style=\"text-align: right;\">\n",
2040:        "      <th></th>\n",
2041:        "      <th>rating</th>\n",
2042:        "      <th>review</th>\n",
2043:        "      <th>label</th>\n",
2044:        "    </tr>\n",
2045:        "  </thead>\n",
2046:        "  <tbody>\n",
2047:        "    <tr>\n",
2048:        "      <th>1</th>\n",
2049:        "      <td>2</td>\n",
2050:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2051:        "      <td>0</td>\n",
2052:        "    </tr>\n",
2053:        "    <tr>\n",
2054:        "      <th>2</th>\n",
2055:        "      <td>3</td>\n",
2056:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2057:        "      <td>0</td>\n",
2058:        "    </tr>\n",
2059:        "    <tr>\n",
2060:        "      <th>3</th>\n",
2061:        "      <td>2</td>\n",
2062:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2063:        "      <td>0</td>\n",
2064:        "    </tr>\n",
2065:        "    <tr>\n",
2066:        "      <th>5</th>\n",
2067:        "      <td>1</td>\n",
2068:        "      <td>i went to this restaurant last saturday based on the reviews that my friend saw on yelp well i can easily say that this is the worst food i have ever eaten at a restaurant i have no idea what thos...</td>\n",
2069:        "      <td>1</td>\n",
2070:        "    </tr>\n",
2071:        "    <tr>\n",
2072:        "      <th>6</th>\n",
2073:        "      <td>4</td>\n",
2074:        "      <td>place was nice looking staff were friendly and food was delicious we were seated in the main dining area as there were no seats available in the back yard a c was pumping and place was a bit chill...</td>\n",
2075:        "      <td>0</td>\n",
2076:        "    </tr>\n",
2077:        "    <tr>\n",
2078:        "      <th>...</th>\n",
2079:        "      <td>...</td>\n",
2080:        "      <td>...</td>\n",
2081:        "      <td>...</td>\n",
2082:        "    </tr>\n",
2083:        "    <tr>\n",
2084:        "      <th>49988</th>\n",
2085:        "      <td>3</td>\n",
2086:        "      <td>good very inexpensive basic cantonese food you can even eat healthy here if you are careful about what you order more of a lunch place than dinner if you care about cleanliness you will mind the s...</td>\n",
2087:        "      <td>0</td>\n",
2088:        "    </tr>\n",
2089:        "    <tr>\n",
2090:        "      <th>49989</th>\n",
2091:        "      <td>2</td>\n",
2092:        "      <td>david chang you may be slightly overrated went with a group of six we ordered 1 the kimchee w pears 2 hamachi 3 oysters w kimchee foam 4 the pork buns and of course 5 the pork shoulder the best by...</td>\n",
2093:        "      <td>1</td>\n",
2094:        "    </tr>\n",
2095:        "    <tr>\n",
2096:        "      <th>49990</th>\n",
2097:        "      <td>5</td>\n",
2098:        "      <td>first went to soco a few weeks before the grand opening the grand opening was in late july so im guessing late june is when i first went they were only open sporadically then and they were testing...</td>\n",
2099:        "      <td>1</td>\n",
2100:        "    </tr>\n",
2101:        "    <tr>\n",
2102:        "      <th>49992</th>\n",
2103:        "      <td>5</td>\n",
2104:        "      <td>a friend was in town and i learned this was her spot the must do thing on the line up having never been sounded good to me everything was under complete control here you walked in and you either h...</td>\n",
2105:        "      <td>1</td>\n",
2106:        "    </tr>\n",
2107:        "    <tr>\n",
2108:        "      <th>49998</th>\n",
2109:        "      <td>5</td>\n",
2110:        "      <td>laissez les bons temps rouler who on earth would ever guess that this place would be on satan s island if it weren t for the b f living here i wouldn t visit or pay the toll but for bayou i would ...</td>\n",
2111:        "      <td>0</td>\n",
2112:        "    </tr>\n",
2113:        "  </tbody>\n",
2114:        "</table>\n",
2115:        "<p>18962 rows × 3 columns</p>\n",
2116:        "</div>"
2117:       ],
2118:       "text/plain": [
2119:        "       rating  \\\n",
2120:        "1           2   \n",
2121:        "2           3   \n",
2122:        "3           2   \n",
2123:        "5           1   \n",
2124:        "6           4   \n",
2125:        "...       ...   \n",
2126:        "49988       3   \n",
2127:        "49989       2   \n",
2128:        "49990       5   \n",
2129:        "49992       5   \n",
2130:        "49998       5   \n",
2131:        "\n",
2132:        "                                                                                                                                                                                                        review  \\\n",
2133:        "1      the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2134:        "2      very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2135:        "3      i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2136:        "5      i went to this restaurant last saturday based on the reviews that my friend saw on yelp well i can easily say that this is the worst food i have ever eaten at a restaurant i have no idea what thos...   \n",
2137:        "6      place was nice looking staff were friendly and food was delicious we were seated in the main dining area as there were no seats available in the back yard a c was pumping and place was a bit chill...   \n",
2138:        "...                                                                                                                                                                                                        ...   \n",
2139:        "49988  good very inexpensive basic cantonese food you can even eat healthy here if you are careful about what you order more of a lunch place than dinner if you care about cleanliness you will mind the s...   \n",
2140:        "49989  david chang you may be slightly overrated went with a group of six we ordered 1 the kimchee w pears 2 hamachi 3 oysters w kimchee foam 4 the pork buns and of course 5 the pork shoulder the best by...   \n",
2141:        "49990  first went to soco a few weeks before the grand opening the grand opening was in late july so im guessing late june is when i first went they were only open sporadically then and they were testing...   \n",
2142:        "49992  a friend was in town and i learned this was her spot the must do thing on the line up having never been sounded good to me everything was under complete control here you walked in and you either h...   \n",
2143:        "49998  laissez les bons temps rouler who on earth would ever guess that this place would be on satan s island if it weren t for the b f living here i wouldn t visit or pay the toll but for bayou i would ...   \n",
2144:        "\n",
2145:        "       label  \n",
2146:        "1          0  \n",
2147:        "2          0  \n",
2148:        "3          0  \n",
2149:        "5          1  \n",
2150:        "6          0  \n",
2151:        "...      ...  \n",
2152:        "49988      0  \n",
2153:        "49989      1  \n",
2154:        "49990      1  \n",
2155:        "49992      1  \n",
2156:        "49998      0  \n",
2157:        "\n",
2158:        "[18962 rows x 3 columns]"
2159:       ]
2160:      },
2161:      "execution_count": 547,
2162:      "metadata": {},
2163:      "output_type": "execute_result"
2164:     }
2165:    ],
2166:    "source": [
2167:     "yelp_sample[yelp_sample[\"review\"].str.len() > 500]"
2168:    ]
2169:   },
2170:   {
2171:    "cell_type": "markdown",
2172:    "id": "86a3f1c5",
2173:    "metadata": {},
2174:    "source": [
2175:     "When detecting AI-generated reviews, very short texts provide insufficient linguistic signal to reliably distinguish between human and AI."
2176:    ]
2177:   },
2178:   {
2179:    "cell_type": "code",
2180:    "execution_count": 548,
2181:    "id": "f1b0f41e",
2182:    "metadata": {},
2183:    "outputs": [],
2184:    "source": [
2185:     "yelp_sample = yelp_sample[yelp_sample[\"review\"].str.len() >= 20]"
2186:    ]
2187:   },
2188:   {
2189:    "cell_type": "code",
2190:    "execution_count": 549,
2191:    "id": "49439f21",
2192:    "metadata": {},
2193:    "outputs": [],
2194:    "source": [
2195:     "amazon_df=amazon_df[amazon_df[\"review\"].str.len() >= 20]"
2196:    ]
2197:   },
2198:   {
2199:    "cell_type": "code",
2200:    "execution_count": 550,
2201:    "id": "e54669f8",
2202:    "metadata": {},
2203:    "outputs": [
2204:     {
2205:      "name": "stdout",
2206:      "output_type": "stream",
2207:      "text": [
2208:       "Empty Reviews : 0\n",
2209:       "Average Review Length : 535.9302043293546\n",
2210:       "Shortest Review Length : 20\n",
2211:       "Longest Review Length : 4907\n"
2212:      ]
2213:     }
2214:    ],
2215:    "source": [
2216:     "#yelp\n",
2217:     "\n",
2218:     "print(\"Empty Reviews :\", (yelp_sample[\"review\"] == \"\").sum())\n",
2219:     "\n",
2220:     "print(\"Average Review Length :\", yelp_sample[\"review\"].str.len().mean())\n",
2221:     "\n",
2222:     "print(\"Shortest Review Length :\", yelp_sample[\"review\"].str.len().min())\n",
2223:     "\n",
2224:     "print(\"Longest Review Length :\", yelp_sample[\"review\"].str.len().max())"
2225:    ]
2226:   },
2227:   {
2228:    "cell_type": "code",
2229:    "execution_count": 551,
2230:    "id": "a1ac3c21",
2231:    "metadata": {},
2232:    "outputs": [
2233:     {
2234:      "name": "stdout",
2235:      "output_type": "stream",
2236:      "text": [
2237:       "Empty Reviews : 0\n",
2238:       "Average Review Length : 339.9354319796075\n",
2239:       "Shortest Review Length : 24\n",
2240:       "Longest Review Length : 2095\n"
2241:      ]
2242:     }
2243:    ],
2244:    "source": [
2245:     "#amazon\n",
2246:     "\n",
2247:     "print(\"Empty Reviews :\", (amazon_df[\"review\"] == \"\").sum())\n",
2248:     "\n",
2249:     "print(\"Average Review Length :\", amazon_df[\"review\"].str.len().mean())\n",
2250:     "\n",
2251:     "print(\"Shortest Review Length :\", amazon_df[\"review\"].str.len().min())\n",
2252:     "\n",
2253:     "print(\"Longest Review Length :\", amazon_df[\"review\"].str.len().max())"
2254:    ]
2255:   },
2256:   {
2257:    "cell_type": "markdown",
2258:    "id": "afeac13d",
2259:    "metadata": {},
2260:    "source": [
2261:     "### Exploratory Data Analysis"
2262:    ]
2263:   },
2264:   {
2265:    "cell_type": "code",
2266:    "execution_count": 552,
2267:    "id": "fa86f547",
2268:    "metadata": {},
2269:    "outputs": [
2270:     {
2271:      "name": "stderr",
2272:      "output_type": "stream",
2273:      "text": [
2274:       "/opt/python-venvs/work/lib/python3.12/site-packages/nltk/downloader.py:1076: UserWarning: NLTK will not authorize the non-private download directory '/home/hitesh/nltk_data': it (or an ancestor) is world- or group-writable, so another local user could plant files there. Choose a private location such as ~/nltk_data.\n",
2275:       "  for msg in self.incr_download(info_or_id, download_dir, force):\n",
2276:       "[nltk_data] Downloading package punkt to /home/hitesh/nltk_data...\n",
2277:       "[nltk_data]   Package punkt is already up-to-date!\n",
2278:       "[nltk_data] Downloading package punkt_tab to /home/hitesh/nltk_data...\n",
2279:       "[nltk_data]   Package punkt_tab is already up-to-date!\n"
2280:      ]
2281:     },
2282:     {
2283:      "data": {
2284:       "text/plain": [
2285:        "True"
2286:       ]
2287:      },
2288:      "execution_count": 552,
2289:      "metadata": {},
2290:      "output_type": "execute_result"
2291:     }
2292:    ],
2293:    "source": [
2294:     "import matplotlib.pyplot as plt\n",
2295:     "from wordcloud import WordCloud\n",
2296:     "from collections import Counter\n",
2297:     "from sklearn.feature_extraction.text import CountVectorizer\n",
2298:     "import nltk\n",
2299:     "\n",
2300:     "nltk.download(\"punkt\")\n",
2301:     "nltk.download(\"punkt_tab\")"
2302:    ]
2303:   },
2304:   {
2305:    "cell_type": "code",
2306:    "execution_count": 553,
2307:    "id": "3a88a628",
2308:    "metadata": {},
2309:    "outputs": [
2310:     {
2311:      "name": "stdout",
2312:      "output_type": "stream",
2313:      "text": [
2314:       "Dataset Shape : (40407, 3)\n",
2315:       "\n",
2316:       "Class Distribution:\n",
2317:       "\n",
2318:       "label\n",
2319:       "0    20215\n",
2320:       "1    20192\n",
2321:       "Name: count, dtype: int64\n"
2322:      ]
2323:     },
2324:     {
2325:      "data": {
2326:       "text/html": [
2327:        "<div>\n",
2328:        "<style scoped>\n",
2329:        "    .dataframe tbody tr th:only-of-type {\n",
2330:        "        vertical-align: middle;\n",
2331:        "    }\n",
2332:        "\n",
2333:        "    .dataframe tbody tr th {\n",
2334:        "        vertical-align: top;\n",
2335:        "    }\n",
2336:        "\n",
2337:        "    .dataframe thead th {\n",
2338:        "        text-align: right;\n",
2339:        "    }\n",
2340:        "</style>\n",
2341:        "<table border=\"1\" class=\"dataframe\">\n",
2342:        "  <thead>\n",
2343:        "    <tr style=\"text-align: right;\">\n",
2344:        "      <th></th>\n",
2345:        "      <th>rating</th>\n",
2346:        "      <th>review</th>\n",
2347:        "      <th>label</th>\n",
2348:        "    </tr>\n",
2349:        "  </thead>\n",
2350:        "  <tbody>\n",
2351:        "    <tr>\n",
2352:        "      <th>0</th>\n",
2353:        "      <td>5</td>\n",
2354:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2355:        "      <td>1</td>\n",
2356:        "    </tr>\n",
2357:        "    <tr>\n",
2358:        "      <th>1</th>\n",
2359:        "      <td>5</td>\n",
2360:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2361:        "      <td>1</td>\n",
2362:        "    </tr>\n",
2363:        "    <tr>\n",
2364:        "      <th>2</th>\n",
2365:        "      <td>5</td>\n",
2366:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2367:        "      <td>1</td>\n",
2368:        "    </tr>\n",
2369:        "    <tr>\n",
2370:        "      <th>3</th>\n",
2371:        "      <td>1</td>\n",
2372:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2373:        "      <td>1</td>\n",
2374:        "    </tr>\n",
2375:        "    <tr>\n",
2376:        "      <th>4</th>\n",
2377:        "      <td>5</td>\n",
2378:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2379:        "      <td>1</td>\n",
2380:        "    </tr>\n",
2381:        "  </tbody>\n",
2382:        "</table>\n",
2383:        "</div>"
2384:       ],
2385:       "text/plain": [
2386:        "   rating  \\\n",
2387:        "0       5   \n",
2388:        "1       5   \n",
2389:        "2       5   \n",
2390:        "3       1   \n",
2391:        "4       5   \n",
2392:        "\n",
2393:        "                                                                                review  \\\n",
2394:        "0                love this well made sturdy and very comfortable i love it very pretty   \n",
2395:        "1        love it a great upgrade from the original i ve had mine for a couple of years   \n",
2396:        "2                    this pillow saved my back i love the look and feel of this pillow   \n",
2397:        "3       missing information on how to use it but it is a great product for the price i   \n",
2398:        "4  very nice set good quality we have had the set for two months now and have not been   \n",
2399:        "\n",
2400:        "   label  \n",
2401:        "0      1  \n",
2402:        "1      1  \n",
2403:        "2      1  \n",
2404:        "3      1  \n",
2405:        "4      1  "
2406:       ]
2407:      },
2408:      "execution_count": 553,
2409:      "metadata": {},
2410:      "output_type": "execute_result"
2411:     }
2412:    ],
2413:    "source": [
2414:     "#amazon\n",
2415:     "\n",
2416:     "print(\"Dataset Shape :\", amazon_df.shape)\n",
2417:     "print(\"\\nClass Distribution:\\n\")\n",
2418:     "print(amazon_df[\"label\"].value_counts())\n",
2419:     "\n",
2420:     "amazon_df.head()"
2421:    ]
2422:   },
2423:   {
2424:    "cell_type": "code",
2425:    "execution_count": 554,
2426:    "id": "b98ee1c0",
2427:    "metadata": {},
2428:    "outputs": [
2429:     {
2430:      "name": "stdout",
2431:      "output_type": "stream",
2432:      "text": [
2433:       "Dataset Shape : (49430, 3)\n",
2434:       "\n",
2435:       "Class Distribution:\n",
2436:       "\n",
2437:       "label\n",
2438:       "0    24883\n",
2439:       "1    24547\n",
2440:       "Name: count, dtype: int64\n"
2441:      ]
2442:     },
2443:     {
2444:      "data": {
2445:       "text/html": [
2446:        "<div>\n",
2447:        "<style scoped>\n",
2448:        "    .dataframe tbody tr th:only-of-type {\n",
2449:        "        vertical-align: middle;\n",
2450:        "    }\n",
2451:        "\n",
2452:        "    .dataframe tbody tr th {\n",
2453:        "        vertical-align: top;\n",
2454:        "    }\n",
2455:        "\n",
2456:        "    .dataframe thead th {\n",
2457:        "        text-align: right;\n",
2458:        "    }\n",
2459:        "</style>\n",
2460:        "<table border=\"1\" class=\"dataframe\">\n",
2461:        "  <thead>\n",
2462:        "    <tr style=\"text-align: right;\">\n",
2463:        "      <th></th>\n",
2464:        "      <th>rating</th>\n",
2465:        "      <th>review</th>\n",
2466:        "      <th>label</th>\n",
2467:        "    </tr>\n",
2468:        "  </thead>\n",
2469:        "  <tbody>\n",
2470:        "    <tr>\n",
2471:        "      <th>0</th>\n",
2472:        "      <td>5</td>\n",
2473:        "      <td>my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...</td>\n",
2474:        "      <td>1</td>\n",
2475:        "    </tr>\n",
2476:        "    <tr>\n",
2477:        "      <th>1</th>\n",
2478:        "      <td>2</td>\n",
2479:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2480:        "      <td>0</td>\n",
2481:        "    </tr>\n",
2482:        "    <tr>\n",
2483:        "      <th>2</th>\n",
2484:        "      <td>3</td>\n",
2485:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2486:        "      <td>0</td>\n",
2487:        "    </tr>\n",
2488:        "    <tr>\n",
2489:        "      <th>3</th>\n",
2490:        "      <td>2</td>\n",
2491:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2492:        "      <td>0</td>\n",
2493:        "    </tr>\n",
2494:        "    <tr>\n",
2495:        "      <th>4</th>\n",
2496:        "      <td>5</td>\n",
2497:        "      <td>my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried</td>\n",
2498:        "      <td>1</td>\n",
2499:        "    </tr>\n",
2500:        "  </tbody>\n",
2501:        "</table>\n",
2502:        "</div>"
2503:       ],
2504:       "text/plain": [
2505:        "   rating  \\\n",
2506:        "0       5   \n",
2507:        "1       2   \n",
2508:        "2       3   \n",
2509:        "3       2   \n",
2510:        "4       5   \n",
2511:        "\n",
2512:        "                                                                                                                                                                                                    review  \\\n",
2513:        "0  my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...   \n",
2514:        "1  the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2515:        "2  very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2516:        "3  i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2517:        "4                                                my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried   \n",
2518:        "\n",
2519:        "   label  \n",
2520:        "0      1  \n",
2521:        "1      0  \n",
2522:        "2      0  \n",
2523:        "3      0  \n",
2524:        "4      1  "
2525:       ]
2526:      },
2527:      "execution_count": 554,
2528:      "metadata": {},
2529:      "output_type": "execute_result"
2530:     }
2531:    ],
2532:    "source": [
2533:     "#Yelp\n",
2534:     "\n",
2535:     "print(\"Dataset Shape :\", yelp_sample.shape)\n",
2536:     "print(\"\\nClass Distribution:\\n\")\n",
2537:     "print(yelp_sample[\"label\"].value_counts())\n",
2538:     "\n",
2539:     "yelp_sample.head()"
2540:    ]
2541:   },
2542:   {
2543:    "cell_type": "code",
2544:    "execution_count": 586,
2545:    "id": "c94a51a5",
2546:    "metadata": {},
2547:    "outputs": [
2548:     {
2549:      "data": {
2550:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAi8AAAF1CAYAAAAgKQpIAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUMhJREFUeJzt3XdYFNf6B/Av0kSQZsGGQMQSu1hQEUEpFuxiNIolAkZjTKyJJWo015ZyjRpvLCAxGjX2WGJDxY7KtYtdKTakyKKCSzu/P7zMz3EBl3VhWfP9PM8+T/bMO2fe3XvHfTlz5oyBEEKAiIiISE+U0XUCREREREXB4oWIiIj0CosXIiIi0issXoiIiEivsHghIiIivcLihYiIiPQKixciIiLSKyxeiIiISK+weCF6zfXr1xESEoL09HSdHe/SpUsICQlBZmZmieRQUB6l1Y0bN7Bx40aEhIQgPj5e1+mQhhQKBUJCQnDnzh1dp0J6yEjXCRAVl7t37+LQoUPSexMTE1hZWaFOnTqoW7cuypRRrd0jIiIwatQodO7cGeXKlVP7WFevXsWpU6cwaNAgmJmZqb1ffsf7+++/MWXKFPj7+8PExETtvt4lR00/d0n78ccfMX36dHTv3h2WlpZo1aoV7O3tC90nISEBO3fuhK2tLfr06VNCmeqHN88RQ0NDVKhQAa6urrCzsyvWYz969AjBwcFYs2YNatWqVazHovcPixd6b505cwbBwcHw8vKCo6MjcnJykJSUhKioKADAqFGj8PXXX8PU1FTa58MPP0RgYCDMzc2LdKwDBw5g3Lhx6NatW5GKF02Pp4nCcizJPDSVlZWFGTNmYNy4cZg7d67a+y1duhTfffcdDA0NERMTgxo1ahRjlvrlzXMkMzMTFy9exNWrVzFhwgQsWLCg2I5tbW2NwMBAODs7F9sx6P3F4oXeeyNHjoS/v7/0Pjc3F2vWrMGoUaNw6NAh7N+/Xxrh8PDwgIeHR4nlVtLHK+15FCY+Ph4ZGRlF+is9JycHYWFh6N69Ow4cOICwsDBMnz69GLPUT6+fI0IIjBw5Et9//z3atGmDXr16Fcsxq1SpgpCQkGLpm95/LF7oH6dMmTIYOnQo0tPT8dlnn+E///kPxo4dC+DV3I/jx49j4MCBsssnz58/x8mTJ5GYmIiaNWuiRYsW0uhFZGQkIiMjAQDr1q2DpaUlAMDPzw9Vq1bFpUuXcObMGQwZMgTZ2dk4ePAgkpOTMWzYsAKPl+fZs2cIDw9HZmYm2rdvj6pVq8q2nzp1Cjdv3sTQoUNl7bGxsThw4AB69uyJSpUqvTXHwvJ48OABTp06hZcvX6Ju3bpo0aIFDAwMpO1vfr4DBw4gPT0d7u7uRRrlKOw4R48eRUREBADgxIkTEELA3NwcH3/8caF97t27F/fv38fmzZtha2uL0NBQTJs2TeWS4eufQalUIjw8HADg6+srjUY9e/YMhw4dglKphJeXFypUqJDvdw4ABgYGKFeuHBo0aIDGjRtLMUqlEmvWrCkw3759+8LGxkat7+TNvN/lu3+dgYEBPv30U6xYsQL79u1TKV6ysrJw6tQpxMbGwsrKCu7u7lLOycnJ2LZtG9q0aYMGDRqo9L1u3TpUrFgRvr6+UCgU2LRpEzp06KBSkBZ2DCEEwsLC0LhxY7Ro0ULaZ+fOnUhISMBHH30k/f87NTUVmzdvhqenpzTCk5ubi1OnTiEuLg62trZwcXFBpUqVNPquSIcE0Xtq/fr1AoDYtGlTvttfvnwpzM3NhYuLi9T266+/CgAiPj5eatuxY4ewsrISzZs3FwEBAaJDhw6idu3aYv/+/UIIITZs2CBat24tAIiBAweKwMBAERgYKK5fvy6EEGLevHkCgDh06JBo0qSJ6NOnj3B0dCzweHnx4eHholGjRsLf3180bdpUmJqaimXLlsk+w+jRo4W5ubnKZ9u2bZsAIE6dOqVWjvnlkZubKyZM... (line truncated to 2000 chars)
2551:       "text/plain": [
2552:        "<Figure size 600x400 with 1 Axes>"
2553:       ]
2554:      },
2555:      "metadata": {},
2556:      "output_type": "display_data"
2557:     }
2558:    ],
2559:    "source": [
2560:     "label_counts = amazon_df[\"label\"].value_counts().sort_index()\n",
2561:     "\n",
2562:     "plt.figure(figsize=(6,4))\n",
2563:     "plt.bar([\"Genuine (0)\", \"AI Generated (1)\"], label_counts.values)\n",
2564:     "plt.title(\"Distribution of Amazon Reviews\")\n",
2565:     "plt.ylabel(\"Number of Reviews\")\n",
2566:     "\n",
2567:     "for i, value in enumerate(label_counts.values):\n",
2568:     "    plt.text(i, value, str(value), ha=\"center\", va=\"bottom\")\n",
2569:     "\n",
2570:     "plt.show()"
2571:    ]
2572:   },
2573:   {
2574:    "cell_type": "code",
2575:    "execution_count": 587,
2576:    "id": "c8e7b73f",
2577:    "metadata": {},
2578:    "outputs": [
2579:     {
2580:      "data": {
2581:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAi8AAAF1CAYAAAAgKQpIAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAR3VJREFUeJzt3XdYFNf+BvAX6UWwYUdQsATFghURpaPYBaNeNcbeNTHxqkksGCOa5k2MNxp7LLH3xB7RxIIYwKhY0KhgCUGRRaXD+f3hZX6MS1nWhWX0/TzPPE/2zJkz312zuy+zZ2YMhBACRERERApRQd8FEBEREZUEwwsREREpCsMLERERKQrDCxERESkKwwsREREpCsMLERERKQrDCxERESkKwwsREREpCsMLUSnYu3cvDh8+rNf9bd++HcePHy+zGgqrozzKzs5GWFgY1q1bh82bN5fqvoQQWLVqFSIjI0t1P2XpwIED+Pnnn/VdBr3BDHiFXaKiHTx4EPfv3wcAGBgYwNLSEra2tnBxcUH16tUL3KZNmzaoVq0aDh06VKJ97dq1C1ZWVvD39y/RdgXtz8nJCS1btsSOHTtKNNar1Kjt8y5L6enpcHd3R3JyMjp37owqVargq6++kvWJi4vDkSNH0Lp1a7Rq1arAcTZt2gQjIyMMGDCgyP1lZ2fD2NgYc+fOxbx583T1NLB+/XpkZWUBePH/pYWFBZo0aVJovbrUqVMnGBkZISwsrNT3RVQQI30XQFTeffXVV/jtt98wdOhQAEBaWhri4uJw4cIFuLq6IiQkBL6+vrJt+vTpAysrqxLva86cOXBwcChxeNF2f9ooqsayrENbW7ZsQWRkJG7duoUGDRoU2KdWrVpYvnw5Hjx4gEuXLqFq1aqy9T/88APGjh2LlStXlkXJBZo4cSIqV66MgIAAAMCDBw9w7NgxNG/eHLt374adnV2p7btnz56oUIEH7kmPBBEVycfHR9jY2Ki1//PPP2LgwIECgFi1apVO9tW0aVPRvXt3nYzl6OgogoKCdDJWfrqsUR9mzZolKlSoIHJzc4vsd/XqVWFubq72Gt68eVNYWVmJXr16abS/rKwsAUDMnTtX25ILZGlpKQICAmRtZ86cERUqVFD0vw+RJnjkhUhLtra22LhxI27duoUpU6agR48eqFGjBoAXcz/MzMykv4rzxMbG4vLly8jOzkbTpk3h7OwsrVu/fj2ePHkCQ0NDrFq1CgBgY2OD/v37A3gxh6VKlSrw8fHBzZs3ERERAQcHB7i5uRW6vzxXr15FZGQkqlevji5dusDExES2ft26dWjSpAk6dOggaz9y5AiePXuGfv36aVRjYXUIIXD+/HnExsbCwsICbm5uqFWrlqzPy8/v/PnzqFKlCry8vGBqalrMv0bx+xFCYPXq1YiIiAAArF69GgDg6uoKV1dXtbGaNGmCxYsXY8qUKVi/fj2GDRuGnJwcvPPOO7CwsJCevxACERERiI2NhampKdzd3dWe28syMjKwYcMGtG/fHi4uLjhz5gz++usvODk5qf0blISbmxtatGiBo0ePQggBAwMD2fqbN28iMjISWVlZaNmyJZo2bSqt27NnD3Jzc6V/6/z++OMPREVFYfDgwTA3N8eBAwdgYGCA7t27q/Utah+///477t69i8GDB0ttN27cwKlTp9CiRQu0bdtWat+/fz8qVKgg28etW7dw6dIlZGZmwtnZGc2aNdPuhSLl02t0IlKAwo685Fm3bp0AIP773/9Kba1bt5b9VZybmyuGDRsmLCwsRI8ePcTAgQOFi4uL8PPzEykpKUIIISZOnCgqV64s7OzsxMiRI8XIkSPFrFmzpDHyjqTMmzdPtG3bVvTo0UNMnTq1wP3l7//JJ5+Idu3aiaCgIGFraysaNWokbt26JetramoqjZVf9+7dRdOmTaXHxdVYUB23b98WrVq1ElWqVBF9+/YV7u7uwtjYWLZd/noXL14s... (line truncated to 2000 chars)
2582:       "text/plain": [
2583:        "<Figure size 600x400 with 1 Axes>"
2584:       ]
2585:      },
2586:      "metadata": {},
2587:      "output_type": "display_data"
2588:     }
2589:    ],
2590:    "source": [
2591:     "label_counts = yelp_sample[\"label\"].value_counts().sort_index()\n",
2592:     "\n",
2593:     "plt.figure(figsize=(6,4))\n",
2594:     "plt.bar([\"Genuine (0)\", \"AI Generated (1)\"], label_counts.values,color=\"red\")\n",
2595:     "plt.title(\"Distribution of Yelp Reviews\")\n",
2596:     "plt.ylabel(\"Number of Reviews\")\n",
2597:     "\n",
2598:     "for i, value in enumerate(label_counts.values):\n",
2599:     "    plt.text(i, value, str(value), ha=\"center\", va=\"bottom\")\n",
2600:     "\n",
2601:     "plt.show()"
2602:    ]
2603:   },
2604:   {
2605:    "cell_type": "markdown",
2606:    "id": "3d85db35",
2607:    "metadata": {},
2608:    "source": [
2609:     "### Feature Engineering"
2610:    ]
2611:   },
2612:   {
2613:    "cell_type": "markdown",
2614:    "id": "d5e65f85",
2615:    "metadata": {},
2616:    "source": [
2617:     "list the features being created: text_length, word_count, sentence_count, vocab_richness, avg_word_len"
2618:    ]
2619:   },
2620:   {
2621:    "cell_type": "code",
2622:    "execution_count": 557,
2623:    "id": "37794fd1",
2624:    "metadata": {},
2625:    "outputs": [
2626:     {
2627:      "data": {
2628:       "text/html": [
2629:        "<div>\n",
2630:        "<style scoped>\n",
2631:        "    .dataframe tbody tr th:only-of-type {\n",
2632:        "        vertical-align: middle;\n",
2633:        "    }\n",
2634:        "\n",
2635:        "    .dataframe tbody tr th {\n",
2636:        "        vertical-align: top;\n",
2637:        "    }\n",
2638:        "\n",
2639:        "    .dataframe thead th {\n",
2640:        "        text-align: right;\n",
2641:        "    }\n",
2642:        "</style>\n",
2643:        "<table border=\"1\" class=\"dataframe\">\n",
2644:        "  <thead>\n",
2645:        "    <tr style=\"text-align: right;\">\n",
2646:        "      <th></th>\n",
2647:        "      <th>review</th>\n",
2648:        "      <th>text_length</th>\n",
2649:        "      <th>word_count</th>\n",
2650:        "      <th>sentence_count</th>\n",
2651:        "    </tr>\n",
2652:        "  </thead>\n",
2653:        "  <tbody>\n",
2654:        "    <tr>\n",
2655:        "      <th>0</th>\n",
2656:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2657:        "      <td>69</td>\n",
2658:        "      <td>13</td>\n",
2659:        "      <td>1</td>\n",
2660:        "    </tr>\n",
2661:        "    <tr>\n",
2662:        "      <th>1</th>\n",
2663:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2664:        "      <td>77</td>\n",
2665:        "      <td>17</td>\n",
2666:        "      <td>1</td>\n",
2667:        "    </tr>\n",
2668:        "    <tr>\n",
2669:        "      <th>2</th>\n",
2670:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2671:        "      <td>65</td>\n",
2672:        "      <td>14</td>\n",
2673:        "      <td>1</td>\n",
2674:        "    </tr>\n",
2675:        "    <tr>\n",
2676:        "      <th>3</th>\n",
2677:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2678:        "      <td>78</td>\n",
2679:        "      <td>17</td>\n",
2680:        "      <td>1</td>\n",
2681:        "    </tr>\n",
2682:        "    <tr>\n",
2683:        "      <th>4</th>\n",
2684:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2685:        "      <td>83</td>\n",
2686:        "      <td>18</td>\n",
2687:        "      <td>1</td>\n",
2688:        "    </tr>\n",
2689:        "  </tbody>\n",
2690:        "</table>\n",
2691:        "</div>"
2692:       ],
2693:       "text/plain": [
2694:        "                                                                                review  \\\n",
2695:        "0                love this well made sturdy and very comfortable i love it very pretty   \n",
2696:        "1        love it a great upgrade from the original i ve had mine for a couple of years   \n",
2697:        "2                    this pillow saved my back i love the look and feel of this pillow   \n",
2698:        "3       missing information on how to use it but it is a great product for the price i   \n",
2699:        "4  very nice set good quality we have had the set for two months now and have not been   \n",
2700:        "\n",
2701:        "   text_length  word_count  sentence_count  \n",
2702:        "0           69          13               1  \n",
2703:        "1           77          17               1  \n",
2704:        "2           65          14               1  \n",
2705:        "3           78          17               1  \n",
2706:        "4           83          18               1  "
2707:       ]
2708:      },
2709:      "execution_count": 557,
2710:      "metadata": {},
2711:      "output_type": "execute_result"
2712:     }
2713:    ],
2714:    "source": [
2715:     "#feature engineering for amazon\n",
2716:     "\n",
2717:     "amazon_df[\"text_length\"] = amazon_df[\"review\"].str.len()\n",
2718:     "\n",
2719:     "amazon_df[\"word_count\"] = amazon_df[\"review\"].str.split().apply(len)\n",
2720:     "\n",
2721:     "amazon_df[\"sentence_count\"] = amazon_df[\"review\"].apply(\n",
2722:     "    lambda x: len([s for s in nltk.sent_tokenize(x) if s.strip()])\n",
2723:     ")\n",
2724:     "\n",
2725:     "amazon_df[[\"review\",\"text_length\", \"word_count\", \"sentence_count\"]].head()"
2726:    ]
2727:   },
2728:   {
2729:    "cell_type": "code",
2730:    "execution_count": 558,
2731:    "id": "6080e6ea",
2732:    "metadata": {},
2733:    "outputs": [
2734:     {
2735:      "data": {
2736:       "text/html": [
2737:        "<div>\n",
2738:        "<style scoped>\n",
2739:        "    .dataframe tbody tr th:only-of-type {\n",
2740:        "        vertical-align: middle;\n",
2741:        "    }\n",
2742:        "\n",
2743:        "    .dataframe tbody tr th {\n",
2744:        "        vertical-align: top;\n",
2745:        "    }\n",
2746:        "\n",
2747:        "    .dataframe thead th {\n",
2748:        "        text-align: right;\n",
2749:        "    }\n",
2750:        "</style>\n",
2751:        "<table border=\"1\" class=\"dataframe\">\n",
2752:        "  <thead>\n",
2753:        "    <tr style=\"text-align: right;\">\n",
2754:        "      <th></th>\n",
2755:        "      <th>review</th>\n",
2756:        "      <th>text_length</th>\n",
2757:        "      <th>word_count</th>\n",
2758:        "      <th>sentence_count</th>\n",
2759:        "    </tr>\n",
2760:        "  </thead>\n",
2761:        "  <tbody>\n",
2762:        "    <tr>\n",
2763:        "      <th>0</th>\n",
2764:        "      <td>my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...</td>\n",
2765:        "      <td>204</td>\n",
2766:        "      <td>40</td>\n",
2767:        "      <td>1</td>\n",
2768:        "    </tr>\n",
2769:        "    <tr>\n",
2770:        "      <th>1</th>\n",
2771:        "      <td>the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...</td>\n",
2772:        "      <td>889</td>\n",
2773:        "      <td>169</td>\n",
2774:        "      <td>1</td>\n",
2775:        "    </tr>\n",
2776:        "    <tr>\n",
2777:        "      <th>2</th>\n",
2778:        "      <td>very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...</td>\n",
2779:        "      <td>522</td>\n",
2780:        "      <td>107</td>\n",
2781:        "      <td>1</td>\n",
2782:        "    </tr>\n",
2783:        "    <tr>\n",
2784:        "      <th>3</th>\n",
2785:        "      <td>i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...</td>\n",
2786:        "      <td>2489</td>\n",
2787:        "      <td>487</td>\n",

(Output capped at 50 KB. Showing lines 1513-2787. Use offset=2788 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 2.8s)

_Thinking:_

Let me continue reading to see the rest of the notebook.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 2788
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
2788:        "      <td>1</td>\n",
2789:        "    </tr>\n",
2790:        "    <tr>\n",
2791:        "      <th>4</th>\n",
2792:        "      <td>my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried</td>\n",
2793:        "      <td>153</td>\n",
2794:        "      <td>32</td>\n",
2795:        "      <td>1</td>\n",
2796:        "    </tr>\n",
2797:        "  </tbody>\n",
2798:        "</table>\n",
2799:        "</div>"
2800:       ],
2801:       "text/plain": [
2802:        "                                                                                                                                                                                                    review  \\\n",
2803:        "0  my wife and i were told to check this place out we did just that last week and it was off the chain good part upscale grocery but not overpriced part i just stepped into italy and part amazing res...   \n",
2804:        "1  the atmosphere is really great with the open kitchen and all but the hostess bartender and so called owner were too cool for school esp when you we made a reservation on opentable for a specific t...   \n",
2805:        "2  very regular thai food the drinks aren t bad but they re pretty weak we came on a friday night and it was really busy so maybe the service wasn t normal but it was pretty horrible no one came to o...   \n",
2806:        "3  i m not one to trash companies and i have loved this restaurant for years this gives them 2 stars instead of 1 i m posting my email which received a response after 2 days claiming they would follo...   \n",
2807:        "4                                                my favorite of the 1 for 4 dumplings spot cause this place gives you 5 dumpling for a dollar and they re the juiciest and tastiest of the ones i ve tried   \n",
2808:        "\n",
2809:        "   text_length  word_count  sentence_count  \n",
2810:        "0          204          40               1  \n",
2811:        "1          889         169               1  \n",
2812:        "2          522         107               1  \n",
2813:        "3         2489         487               1  \n",
2814:        "4          153          32               1  "
2815:       ]
2816:      },
2817:      "execution_count": 558,
2818:      "metadata": {},
2819:      "output_type": "execute_result"
2820:     }
2821:    ],
2822:    "source": [
2823:     "#feature engineering for yelp\n",
2824:     "\n",
2825:     "yelp_sample[\"text_length\"] = yelp_sample[\"review\"].str.len()\n",
2826:     "\n",
2827:     "yelp_sample[\"word_count\"] = yelp_sample[\"review\"].str.split().apply(len)\n",
2828:     "\n",
2829:     "yelp_sample[\"sentence_count\"] = yelp_sample[\"review\"].apply(\n",
2830:     "    lambda x: len([s for s in nltk.sent_tokenize(x) if s.strip()])\n",
2831:     ")\n",
2832:     "\n",
2833:     "yelp_sample[[\"review\",\"text_length\", \"word_count\", \"sentence_count\"]].head()"
2834:    ]
2835:   },
2836:   {
2837:    "cell_type": "markdown",
2838:    "id": "4eb0eefa",
2839:    "metadata": {},
2840:    "source": [
2841:     "### Feature Distributions"
2842:    ]
2843:   },
2844:   {
2845:    "cell_type": "code",
2846:    "execution_count": 600,
2847:    "id": "dd293d5c",
2848:    "metadata": {},
2849:    "outputs": [
2850:     {
2851:      "data": {
2852:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUbpJREFUeJzt3Xd0FWX+x/FPegikQEJLCAk9CBjpKiUSCF0WFlGKIoKKLhZQFmVXsa2L4qK4y1pWBWVdFCxUUQhNioiK9F5CC4FQQkIJkPL8/uAwPy4JcC/c5Abm/Ton52Se+d6Z751c4MPkmRkvY4wRAAAAYCPenm4AAAAAKG6EYAAAANgOIRgAAAC2QwgGAACA7RCCAQAAYDuEYAAAANgOIRgAAAC2QwgGAACA7RCCAVy3xx9/XD169PDo/vr166d+/foVWw+X66MkWr58uXr06KFbb71VcXFxnm6nUBMnTlRcXJxOnDjh6VZuaD169NAjjzzi6TaAGwIhGICDESNGKC4uTnFxcapbt64aN26s9u3ba9iwYVq4cKEKe8jkvn37lJKS4vK+Bg4cqHvuucfl1xW2vz179mjPnj0ub+tqrtTjtb7v4pSamqqkpCRFRkbqf//7n6ZPn37Z2ot/9nFxcbr11lvVuXNnvf/++8rNzS3SPo8ePaqtW7cqLy+vSPdzNV9//bXi4uK0bNkyj/ZxJb1791b//v0LXZeSkqJ9+/YVc0fAjcnX0w0AKFkOHDigrVu3au3atfL399fZs2e1f/9+JScnq1u3boqPj9fUqVMVFRVlveaDDz64ppC0d+9eHT9+3OXXXev+rsWVeizOPq7VggULlJ2drWeffVbVq1e/Yu2lP/usrCzNmTNHTzzxhObNm6dp06YVWZ8DBw5U165dFRISUmT7cMbx48e1detWnTx50qN9XMnu3bsVGBjo6TaAGx4hGEChateubf1DGx8fry5duujhhx9WixYt1KVLF61atUo+Pj6SpCpVqhRrb8W9v8spKX1cycGDByXJpXB58c++WbNm2rFjh/73v/9p7dq1io+PL5I+y5Urp3LlyhXJtgGgMEyHAOC0+vXr6/nnn9fatWv1zTffWOOFzY3du3evhg0bptatW6tp06a6//77HX7F3KFDB61YsUIbN260fv3euHFja/2FOb6ZmZl69tln1bRpUz399NOX3d8FGRkZevLJJ9W4cWMlJiZq4sSJBWratm2rZ599tsD4iy++qDvuuMPpHi/Xx88//6x+/fqpYcOGatasmZ566int3bvXoebC+zt58qSGDx+uJk2aKCEhQRMmTCj0fRXmavu544479I9//MP6Pi4uTi+//LLT27+gUaNGkqRt27Y5jGdmZur111/XXXfdpVtvvVVdu3Z1+FxMnTpVcXFxWrNmTYFtLlmyRHFxcUpOTpZ0+TnBV9vH6tWrFRcXpyVLllhj+/fvV1xcnFq2bOmwrXHjxunWW2/V2bNnXT4Gl9qyZYv+9Kc/qVmzZmrYsKEGDBigjRs3OtRcmJ97/PhxPf3002rcuLHatGmjyZMnF7rNb775Rh06dFDDhg310EMPad++fRoxYoTuuusuq6ZVq1Zau3atfvnlF+sz2apVqwLbcnafgJ0RggG4pFu3bpKkuXPnWmOXzo3NyspSy5YttW7dOr344ov6z3/+o65du+qFF17Q77//Lkl6//33FR8frxo1amj69OmaPn26vvjiC2sbe/bs0a5du9S3b1/Vr19f77zzjmJiYgrd3wV5eXnq16+fmjZtqvfff18JCQl6+OGH9de//tWhbufOnUpNTS3w+rS0NG3fvt1avlqPhfUxZcoUK3y9++67evnll7VixQo1bNhQmzZtKvD+BgwYoAYNGuj9999X8+bNNWjQIE2ZMuVyh9+l/fz3v//VAw88YH0/ffp0Pf7441fd9qUOHDggSSpfvrw1dujQITVp0kSTJk3S448/rgkTJigxMVH3... (line truncated to 2000 chars)
2853:       "text/plain": [
2854:        "<Figure size 800x500 with 1 Axes>"
2855:       ]
2856:      },
2857:      "metadata": {},
2858:      "output_type": "display_data"
2859:     }
2860:    ],
2861:    "source": [
2862:     "plt.figure(figsize=(8,5))\n",
2863:     "\n",
2864:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"word_count\"], bins=40, alpha=0.6, label=\"Genuine\")\n",
2865:     "\n",
2866:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"word_count\"], bins=40, alpha=0.6, label=\"AI Generated\")\n",
2867:     "\n",
2868:     "plt.xlabel(\"Word Count\")\n",
2869:     "plt.ylabel(\"Frequency\")\n",
2870:     "plt.title(\"Distribution of Review Length\")\n",
2871:     "plt.legend()\n",
2872:     "\n",
2873:     "plt.show()"
2874:    ]
2875:   },
2876:   {
2877:    "cell_type": "code",
2878:    "execution_count": 601,
2879:    "id": "679908fd",
2880:    "metadata": {},
2881:    "outputs": [
2882:     {
2883:      "data": {
2884:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUv5JREFUeJzt3Xd8VFX+//F3GoEAKQRCQggh9I7UKAiEIL0IFqQoIBZ0caWpwFoW1BW74rKKiqvruiBYUFCRlkSKgIIoSFN6SSBAQgIhhJTz+4Nf5ssklzADSSbl9Xw85vFwzj1z72fmDvD2zLnnuhljjAAAAADYcXd1AQAAAEBJRFAGAAAALBCUAQAAAAsEZQAAAMACQRkAAACwQFAGAAAALBCUAQAAAAsEZQAAAMACQRmApaefflo33XSTq8solR544AHdcccdLj3esGHDNGrUqGKr4Up1FLdp06bpgQcecGkN5UVUVJSeeOIJp16TkpKiNm3aaNWqVUVUFVC4CMqAiyxevFhNmjTRihUr8m175JFH1KRJEy1cuDDftqefflpNmzbVqVOnirS+hIQE/fnnnw7337dvn/72t7+pR48eat26taKjozV27FgtXbpUOTk5RVipc0aNGqVhw4Y53H/KlClq0qSJmjRpoqZNm6pdu3bq1auXJk+erNjYWFnd3PTIkSM6ePBgkddW0PEOHjyow4cPO72vqymoxmt934Vlx44devXVV3XPPffk25acnKxp06bpxhtvVPv27fXQQw9d8+czZ84c23ci78Pqz+W1Hnvy5Mlq1qyZ0tLS7NpzcnLUtm1bNWnSRPHx8fleFxUVpSFDhlzTe3PG3r17LY9fED8/P3Xr1k2TJk1SdnZ2EVUGFB5PVxcAlFetWrXSnj17tGzZMvXq1cvWbozRwoULdebMGS1dulR33XWX3es+++wz5eTkqHr16sVd8hXNnj1bjz32mPr06aPx48erfv36OnPmjL755hsNHTpUo0eP1ty5c11dpiTp8OHDunDhgsP9jx07pj179uj333+Xh4eHMjIydPToUa1YsUIDBgxQ27ZttWjRIoWEhNheM2/evGsKAc7Wdr3HuxYF1VicdVh5/vnndcMNN6hr16527WfOnNFNN92kSpUq6ZVXXlHlypX17LPPqn379tq4caPq1avn1HFOnTqlPXv2aMuWLfLx8bHbFhAQUGjHrl+/vnbt2qV169apd+/etvYtW7Zo69at8vT0VExMjO6++27btoMHD+qHH37QX//6V6feU3GaNGmS3nrrLX3++ef5/n4DShqCMuAi9evXV3h4uGJiYuzat23bplOnTum+++7TsmXL7LbFx8drz549GjduXHGWWqBFixZp4sSJmj59ul544QW7bd26ddPYsWP1v//9z0XVFZ7GjRvL0/PSX5mtW7dW//79NXbsWHXp0kUDBgzQzz//LHf3Sz/S1a5du1hrK+7jXYkr60hMTNSXX36pV155Jd+2WbNmad++ffrzzz9Vt25dSdLnn3+u+vXr6/HHH9cXX3xxTcds1KiRqlSpUmCf6zl2dHS0JCkmJsYuKMfExKhWrVpq1apVvqCc+/dJ7mtLovDwcHXp0kXvvPMOQRklHlMvABfq3r27tm/fbvdzbUxMjKpXr65HHnlE8fHx2r17t21bbGysJPt/BOPj4zVlyhTdeOONuuGGGzRs2DCtWbPG7jhz585VkyZNlJaWpnfeeUfdunVTu3btbNu/+eYb9evXT23atNHo0aN14MABh+o3xmjq1KkKDw/Xc889Z9mnadOmmjlzpl3bjz/+qBEjRqhNmzaKjIzUhAkTdOTIEbs+V5r/OH36dHXp0sWuLXc+7tmzZzV58mS1a9dOUVFR+s9//mPXr0ePHvrpp5/022+/2X4q79ixo0Pv1Urr1q31+OOP65dfftFXX31la7eaq3vo0CFNmDBBXbp0UYcOHXTPPffoxx9/dLi23Pd45swZ... (line truncated to 2000 chars)
2885:       "text/plain": [
2886:        "<Figure size 800x500 with 1 Axes>"
2887:       ]
2888:      },
2889:      "metadata": {},
2890:      "output_type": "display_data"
2891:     }
2892:    ],
2893:    "source": [
2894:     "# Keep only reviews with <= 50 words\n",
2895:     "short_reviews = amazon_df[amazon_df[\"word_count\"] <= 50]\n",
2896:     "\n",
2897:     "plt.figure(figsize=(8,5))\n",
2898:     "\n",
2899:     "plt.hist(\n",
2900:     "    short_reviews[short_reviews[\"label\"] == 0][\"word_count\"],\n",
2901:     "    bins=50,                 # 1-word bins\n",
2902:     "    alpha=0.6,\n",
2903:     "    label=\"Genuine\"\n",
2904:     ")\n",
2905:     "\n",
2906:     "plt.hist(\n",
2907:     "    short_reviews[short_reviews[\"label\"] == 1][\"word_count\"],\n",
2908:     "    bins=50,\n",
2909:     "    alpha=0.6,\n",
2910:     "    label=\"AI Generated\"\n",
2911:     ")\n",
2912:     "\n",
2913:     "plt.xlim(0, 50)\n",
2914:     "plt.xlabel(\"Word Count\")\n",
2915:     "plt.ylabel(\"Frequency\")\n",
2916:     "plt.title(\"Word Count Distribution (0–50 Words)\")\n",
2917:     "plt.legend()\n",
2918:     "\n",
2919:     "plt.show()"
2920:    ]
2921:   },
2922:   {
2923:    "cell_type": "code",
2924:    "execution_count": 602,
2925:    "id": "1c8f7205",
2926:    "metadata": {},
2927:    "outputs": [
2928:     {
2929:      "data": {
2930:       "text/html": [
2931:        "<div>\n",
2932:        "<style scoped>\n",
2933:        "    .dataframe tbody tr th:only-of-type {\n",
2934:        "        vertical-align: middle;\n",
2935:        "    }\n",
2936:        "\n",
2937:        "    .dataframe tbody tr th {\n",
2938:        "        vertical-align: top;\n",
2939:        "    }\n",
2940:        "\n",
2941:        "    .dataframe thead th {\n",
2942:        "        text-align: right;\n",
2943:        "    }\n",
2944:        "</style>\n",
2945:        "<table border=\"1\" class=\"dataframe\">\n",
2946:        "  <thead>\n",
2947:        "    <tr style=\"text-align: right;\">\n",
2948:        "      <th></th>\n",
2949:        "      <th>review</th>\n",
2950:        "      <th>word_count</th>\n",
2951:        "    </tr>\n",
2952:        "  </thead>\n",
2953:        "  <tbody>\n",
2954:        "    <tr>\n",
2955:        "      <th>0</th>\n",
2956:        "      <td>love this well made sturdy and very comfortable i love it very pretty</td>\n",
2957:        "      <td>13</td>\n",
2958:        "    </tr>\n",
2959:        "    <tr>\n",
2960:        "      <th>1</th>\n",
2961:        "      <td>love it a great upgrade from the original i ve had mine for a couple of years</td>\n",
2962:        "      <td>17</td>\n",
2963:        "    </tr>\n",
2964:        "    <tr>\n",
2965:        "      <th>2</th>\n",
2966:        "      <td>this pillow saved my back i love the look and feel of this pillow</td>\n",
2967:        "      <td>14</td>\n",
2968:        "    </tr>\n",
2969:        "    <tr>\n",
2970:        "      <th>3</th>\n",
2971:        "      <td>missing information on how to use it but it is a great product for the price i</td>\n",
2972:        "      <td>17</td>\n",
2973:        "    </tr>\n",
2974:        "    <tr>\n",
2975:        "      <th>4</th>\n",
2976:        "      <td>very nice set good quality we have had the set for two months now and have not been</td>\n",
2977:        "      <td>18</td>\n",
2978:        "    </tr>\n",
2979:        "    <tr>\n",
2980:        "      <th>...</th>\n",
2981:        "      <td>...</td>\n",
2982:        "      <td>...</td>\n",
2983:        "    </tr>\n",
2984:        "    <tr>\n",
2985:        "      <th>38168</th>\n",
2986:        "      <td>beautiful bootie not real suede but the quality is good the only reason i ordered this is because i had</td>\n",
2987:        "      <td>20</td>\n",
2988:        "    </tr>\n",
2989:        "    <tr>\n",
2990:        "      <th>38227</th>\n",
2991:        "      <td>great shoe very comfy and supportive great quality for the price i am 5 6 and the dress fit perfectly</td>\n",
2992:        "      <td>20</td>\n",
2993:        "    </tr>\n",
2994:        "    <tr>\n",
2995:        "      <th>38269</th>\n",
2996:        "      <td>twelve cotton bandannas in white i love the look and fit of these i am 5 6 and the waistband</td>\n",
2997:        "      <td>20</td>\n",
2998:        "    </tr>\n",
2999:        "    <tr>\n",
3000:        "      <th>38273</th>\n",
3001:        "      <td>cute wings but cheapy made for girls not worth it nice bag very pretty i bought this for my son</td>\n",
3002:        "      <td>20</td>\n",
3003:        "    </tr>\n",
3004:        "    <tr>\n",
3005:        "      <th>39931</th>\n",
3006:        "      <td>input type hidden name value https images na ssl images amazon com images i ffs</td>\n",
3007:        "      <td>15</td>\n",
3008:        "    </tr>\n",
3009:        "  </tbody>\n",
3010:        "</table>\n",
3011:        "<p>5650 rows × 2 columns</p>\n",
3012:        "</div>"
3013:       ],
3014:       "text/plain": [
3015:        "                                                                                                        review  \\\n",
3016:        "0                                        love this well made sturdy and very comfortable i love it very pretty   \n",
3017:        "1                                love it a great upgrade from the original i ve had mine for a couple of years   \n",
3018:        "2                                            this pillow saved my back i love the look and feel of this pillow   \n",
3019:        "3                               missing information on how to use it but it is a great product for the price i   \n",
3020:        "4                          very nice set good quality we have had the set for two months now and have not been   \n",
3021:        "...                                                                                                        ...   \n",
3022:        "38168  beautiful bootie not real suede but the quality is good the only reason i ordered this is because i had   \n",
3023:        "38227    great shoe very comfy and supportive great quality for the price i am 5 6 and the dress fit perfectly   \n",
3024:        "38269             twelve cotton bandannas in white i love the look and fit of these i am 5 6 and the waistband   \n",
3025:        "38273          cute wings but cheapy made for girls not worth it nice bag very pretty i bought this for my son   \n",
3026:        "39931                          input type hidden name value https images na ssl images amazon com images i ffs   \n",
3027:        "\n",
3028:        "       word_count  \n",
3029:        "0              13  \n",
3030:        "1              17  \n",
3031:        "2              14  \n",
3032:        "3              17  \n",
3033:        "4              18  \n",
3034:        "...           ...  \n",
3035:        "38168          20  \n",
3036:        "38227          20  \n",
3037:        "38269          20  \n",
3038:        "38273          20  \n",
3039:        "39931          15  \n",
3040:        "\n",
3041:        "[5650 rows x 2 columns]"
3042:       ]
3043:      },
3044:      "execution_count": 602,
3045:      "metadata": {},
3046:      "output_type": "execute_result"
3047:     }
3048:    ],
3049:    "source": [
3050:     "# AI-generated reviews with 10–20 words\n",
3051:     "ai_reviews_10_20 = amazon_df[\n",
3052:     "    (amazon_df[\"label\"] == 1) &\n",
3053:     "    (amazon_df[\"word_count\"].between(10, 20))\n",
3054:     "]\n",
3055:     "\n",
3056:     "# Display the relevant columns\n",
3057:     "ai_reviews_10_20[[\"review\", \"word_count\"]]"
3058:    ]
3059:   },
3060:   {
3061:    "cell_type": "code",
3062:    "execution_count": 603,
3063:    "id": "4ced490d",
3064:    "metadata": {},
3065:    "outputs": [
3066:     {
3067:      "data": {
3068:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsQAAAHVCAYAAAD2N+0gAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATPBJREFUeJzt3Xd0FXX+//HXTSVACoSaEEIvSlm6irTQq7CiNFEEFRX3SxFZcJVVV8WyKKzYVsGyCoLSFAtNkCIgIL2DgYSQECAhoQRI+fz+4GR+XhIgN9ybBOb5OCfncD/znvm8bybBl8PnzjiMMUYAAACATXkVdgMAAABAYSIQAwAAwNYIxAAAALA1AjEAAABsjUAMAAAAWyMQAwAAwNYIxAAAALA1AjEAAABsjUAM4IY98cQT6tOnT6HON2jQIA0aNKjAerhaH0XR2rVr1adPHzVo0EB16tQp7HZy9cknn6hOnTo6c+ZMYbdyU+vTp48effTRwm4DuOkQiAE4GTdunOrUqaM6deqobt26atKkiTp16qTRo0fr559/Vm4Pt4yNjVV0dLTLcw0dOlR9+/Z1eb/c5jty5IiOHDni8rGu51o95vd9F6S4uDh17NhRYWFh+vLLL7VgwYKr1v753NepU0cNGjRQt27d9P777ysjI8OjfZ46dUr79u1TZmamR+e5nm+++UZ16tTRmjVrCrWPa+nfv78efPDBXLdFR0crNja2gDsCbn4+hd0AgKLl2LFj2rdvn7Zt2yY/Pz9dvHhRR48e1dKlS9WrVy81bNhQc+bMUXh4uLXPBx98kK/AFBMTo9OnT7u8X37ny49r9ViQfeTX8uXLlZaWpqefflrVqlW7Zu2V5z41NVU//PCDnnrqKS1ZskTz58/3WJ9Dhw5Vjx49FBQU5LE58uL06dPat2+fzp49W6h9XMvhw4dVrFixwm4DuKUQiAHkqlatWtZ/dBs2bKju3bvrkUceUcuWLdW9e3dt3rxZ3t7ekqRKlSoVaG8FPd/VFJU+riUhIUGSXAqafz73zZs318GDB/Xll19q27ZtatiwoUf6LF26tEqXLu2RYwPA9bBkAkCe1atXT+PHj9e2bds0d+5cazy3tbQxMTEaPXq0WrdurWbNmumBBx5w+mfozp07a926ddq1a5f1T/RNmjSxtmevCU5JSdHTTz+tZs2aaeTIkVedL1tycrL+9re/qUmTJoqKitInn3ySo6Z9+/Z6+umnc4w///zzuvPOO/Pc49X6WL9+vQYNGqRGjRqpefPm+r//+z/FxMQ41WS/v7Nnz2rs2LFq2rSp2rRpoxkzZuT6vnJzvXnuvPNO/fvf/7b+XKdOHb3wwgt5Pn62xo0bS5L279/vNJ6SkqJXXnlFbdu2VYMGDdSjRw+nn4s5c+aoTp062rp1a45jrlq1SnXq1NHSpUslXX0N8fXm2LJli+rUqaNVq1ZZY0ePHlWdOnV09913Ox1rypQpatCggS5evOjy9+BKe/fu1ZNPPqnmzZurUaNGGjJkiHbt2uVUk72e9/Tp0xo5cqSaNGmidu3aaebMmbkec+7cuercubMaNWqkhx9+WLGxsRo3bpzatm1r1bRq1Urbtm3Tb7/9Zv1MtmrVKsex8jongMsIxABc0qtXL0nS4sWLrbEr19Kmpqbq7rvv1vbt2/X888/rv//9r3r06KHnnntOv//+uyTp/fffV8OGDVW9enUtWLBACxYs0KxZs6xjHDlyRH/88YcGDhyoevXq6e2331ZkZGSu82XLzMzUoEGD1KxZM73//vtq06aNHnnkEf3jH/9wqjt06JDi4uJy7B8fH68DBw5Yr6/XY259zJ492wpiU6dO1QsvvKB169apUaNG2r17d473N2TIENWvX1/vv/++WrRooWHDhmn27NlX+/a7NM///vc/DR482PrzggUL9MQTT1z32Fc6duyYJKls2bLW2PHjx9W0aVN9/vnneuKJJzRjxgxFRUXp... (line truncated to 2000 chars)
3069:       "text/plain": [
3070:        "<Figure size 800x500 with 1 Axes>"
3071:       ]
3072:      },
3073:      "metadata": {},
3074:      "output_type": "display_data"
3075:     }
3076:    ],
3077:    "source": [
3078:     "plt.figure(figsize=(8,5))\n",
3079:     "\n",
3080:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"word_count\"], bins=40, alpha=0.6, label=\"Genuine\")\n",
3081:     "\n",
3082:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"word_count\"], bins=40, alpha=0.6, label=\"AI Generated\")\n",
3083:     "\n",
3084:     "plt.xlabel(\"Word Count\")\n",
3085:     "plt.ylabel(\"Frequency\")\n",
3086:     "plt.title(\"Distribution of Review Length\")\n",
3087:     "plt.legend()\n",
3088:     "\n",
3089:     "plt.show()"
3090:    ]
3091:   },
3092:   {
3093:    "cell_type": "code",
3094:    "execution_count": 604,
3095:    "id": "7e424b9d",
3096:    "metadata": {},
3097:    "outputs": [
3098:     {
3099:      "data": {
3100:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUQlJREFUeJzt3Xd8VFX+//F3QkJCQkhCKCmEEDrSpAZBSAiCFEFQkKaCWEBR6QKruLK6iytiZRVdFHSVZkFBRYoJAioqSFOK0nsNKUASUs7vD36ZL8OEkIFJva/n45GHzrln7v3M3CG8OXPuuW7GGCMAAADAQtyLugAAAACgsBGCAQAAYDmEYAAAAFgOIRgAAACWQwgGAACA5RCCAQAAYDmEYAAAAFgOIRgAAACWQwgGLGjKlCm65ZZbirqMEunhhx9W3759i/R4AwYM0P33319oNVytjsI2adIkPfzww0Vag1XExMToqaeecuo5SUlJatasmVatWlVAVQGuRQgGCsDixYtVv359rVixwmHb448/rvr162vhwoUO26ZMmaIGDRro9OnTBVrfsWPH9Ndff+W7/549e/S3v/1NnTp1UtOmTRUbG6thw4Zp6dKlys7OLsBKnXP//fdrwIAB+e4/btw41a9fX/Xr11eDBg3UokULdenSRWPHjlV8fLxyu6HmoUOHtH///gKvLa/j7d+/XwcPHnR6X9eSV43X+7pd5Y8//tDLL7+s++67z2Hb2bNnNWnSJLVp00YtW7bUiBEjrvv9mTlzpu0zceVPbn8ur/fYY8eO1U033aTz58/btWdnZ6t58+aqX7++jh496vC8mJgY9enT57pemzN2796d6/Hz4u/vr+joaI0ZM0ZZWVkFVBngOh5FXQBQGjVp0kS7du3SsmXL1KVLF1u7MUYLFy5UYmKili5dqv79+9s975NPPlF2drYqVapU2CVf1euvv67x48era9euGjlypGrVqqXExER99dVXuueeezRkyBDNmjWrqMuUJB08eFBpaWn57n/kyBHt2rVLv//+u8qUKaP09HQdPnxYK1as0B133KHmzZtr0aJFCgkJsT1n9uzZ1/UXvLO13ejxrkdeNRZmHbl54YUXdPPNN6tDhw527YmJibrllltUrlw5TZ8+Xb6+vvrHP/6hli1bav369apZs6ZTxzl9+rR27dqljRs3ysfHx25bYGCgy45dq1Yt7dixQ+vWrdPtt99ua9+4caM2bdokDw8PxcXF6d5777Vt279/v77//ns98cQTTr2mwjRmzBi98cYb+vTTTx1+vwHFDSEYKAC1atVSRESE4uLi7Nq3bt2q06dP68EHH9SyZcvsth09elS7du3S8OHDC7PUPC1atEijR4/W5MmT9a9//ctuW3R0tIYNG6aPP/64iKpznXr16snD49Kvw6ZNm6pHjx4aNmyY2rdvrzvuuEO//vqr3N0vfXFWrVq1Qq2tsI93NUVZx8mTJ/X5559r+vTpDtumTZumPXv26K+//lKNGjUkSZ9++qlq1aqlCRMm6LPPPruuY9atW1fly5fPs8+NHDs2NlaSFBcXZxeC4+LiFBoaqiZNmjiE4JzfJznPLY4iIiLUvn17vf3224RgFHtMhwAKSMeOHbVt2za7r1Dj4uJUqVIlPf744zp69Kh27txp2xYfHy/J/i+4o0ePaty4cWrTpo1uvvlmDRgwQGvWrLE7zqxZs1S/fn2dP39eb7/9tqKjo9WiRQvb9q+++krdu3dXs2bNNGTIEO3bty9f9RtjNHHiREVEROj555/PtU+DBg00depUu7Yff/xRgwYNUrNmzRQVFaVRo0bp0KFDdn2uNt9w8uTJat++vV1bzvzXlJQUjR07Vi1atFBMTIw++OADu36dOnXSL7/8oi1btti+vm7dunW+XmtumjZtqgkTJui3337TF198YWvPbW7sgQMHNGrUKLVv316tWrXSfffdpx9//DHfteW8xsTERI0Z... (line truncated to 2000 chars)
3101:       "text/plain": [
3102:        "<Figure size 800x500 with 1 Axes>"
3103:       ]
3104:      },
3105:      "metadata": {},
3106:      "output_type": "display_data"
3107:     }
3108:    ],
3109:    "source": [
3110:     "# Keep only reviews with <= 50 words\n",
3111:     "short_reviews = yelp_sample[yelp_sample[\"word_count\"] <= 50]\n",
3112:     "\n",
3113:     "plt.figure(figsize=(8,5))\n",
3114:     "\n",
3115:     "plt.hist(\n",
3116:     "    short_reviews[short_reviews[\"label\"] == 0][\"word_count\"],\n",
3117:     "    bins=50,                 # 1-word bins\n",
3118:     "    alpha=0.6,\n",
3119:     "    label=\"Genuine\"\n",
3120:     ")\n",
3121:     "\n",
3122:     "plt.hist(\n",
3123:     "    short_reviews[short_reviews[\"label\"] == 1][\"word_count\"],\n",
3124:     "    bins=50,\n",
3125:     "    alpha=0.6,\n",
3126:     "    label=\"AI Generated\"\n",
3127:     ")\n",
3128:     "\n",
3129:     "plt.xlim(0, 50)\n",
3130:     "plt.xlabel(\"Word Count\")\n",
3131:     "plt.ylabel(\"Frequency\")\n",
3132:     "plt.title(\"Word Count Distribution (0–50 Words)\")\n",
3133:     "plt.legend()\n",
3134:     "\n",
3135:     "plt.show()"
3136:    ]
3137:   },
3138:   {
3139:    "cell_type": "code",
3140:    "execution_count": 605,
3141:    "id": "71b4e070",
3142:    "metadata": {},
3143:    "outputs": [
3144:     {
3145:      "data": {
3146:       "text/html": [
3147:        "<div>\n",
3148:        "<style scoped>\n",
3149:        "    .dataframe tbody tr th:only-of-type {\n",
3150:        "        vertical-align: middle;\n",
3151:        "    }\n",
3152:        "\n",
3153:        "    .dataframe tbody tr th {\n",
3154:        "        vertical-align: top;\n",
3155:        "    }\n",
3156:        "\n",
3157:        "    .dataframe thead th {\n",
3158:        "        text-align: right;\n",
3159:        "    }\n",
3160:        "</style>\n",
3161:        "<table border=\"1\" class=\"dataframe\">\n",
3162:        "  <thead>\n",
3163:        "    <tr style=\"text-align: right;\">\n",
3164:        "      <th></th>\n",
3165:        "      <th>review</th>\n",
3166:        "      <th>word_count</th>\n",
3167:        "    </tr>\n",
3168:        "  </thead>\n",
3169:        "  <tbody>\n",
3170:        "    <tr>\n",
3171:        "      <th>11</th>\n",
3172:        "      <td>great burgers a bit of a too cool for school vibe but overall good experience</td>\n",
3173:        "      <td>15</td>\n",
3174:        "    </tr>\n",
3175:        "    <tr>\n",
3176:        "      <th>28</th>\n",
3177:        "      <td>the best ramen i ve ever had really worth waiting for a long time</td>\n",
3178:        "      <td>14</td>\n",
3179:        "    </tr>\n",
3180:        "    <tr>\n",
3181:        "      <th>87</th>\n",
3182:        "      <td>lively atmosphere great to go with a group of friends the burgers are delicious</td>\n",
3183:        "      <td>14</td>\n",
3184:        "    </tr>\n",
3185:        "    <tr>\n",
3186:        "      <th>93</th>\n",
3187:        "      <td>sophies is amazing i can no lt get enough of there empanadas everything in there is delicious</td>\n",
3188:        "      <td>17</td>\n",
3189:        "    </tr>\n",
3190:        "    <tr>\n",
3191:        "      <th>133</th>\n",
3192:        "      <td>a great japanese place for some japanese fusion cuisine whenever i go here this place never fails to amaze me</td>\n",
3193:        "      <td>20</td>\n",
3194:        "    </tr>\n",
3195:        "    <tr>\n",
3196:        "      <th>...</th>\n",
3197:        "      <td>...</td>\n",
3198:        "      <td>...</td>\n",
3199:        "    </tr>\n",
3200:        "    <tr>\n",
3201:        "      <th>49863</th>\n",
3202:        "      <td>i didnt like it ive tasted much better all bread and no meat</td>\n",
3203:        "      <td>13</td>\n",
3204:        "    </tr>\n",
3205:        "    <tr>\n",
3206:        "      <th>49870</th>\n",
3207:        "      <td>great for sunday brunch loved sitting on the outside garden really good eggs benedict</td>\n",
3208:        "      <td>14</td>\n",
3209:        "    </tr>\n",
3210:        "    <tr>\n",
3211:        "      <th>49871</th>\n",
3212:        "      <td>fantastic izakaya extensive sake menu great ambience excellent grilled squid miso rice balls and authentic japanese service</td>\n",
3213:        "      <td>17</td>\n",
3214:        "    </tr>\n",
3215:        "    <tr>\n",
3216:        "      <th>49919</th>\n",
3217:        "      <td>absolutely the best coffee in the neighborhood quality sake served with a passion</td>\n",
3218:        "      <td>13</td>\n",
3219:        "    </tr>\n",
3220:        "    <tr>\n",
3221:        "      <th>49944</th>\n",
3222:        "      <td>ok this is a small place but you will go satisfied very satisfied everything they make is fresh and yummy</td>\n",
3223:        "      <td>20</td>\n",
3224:        "    </tr>\n",
3225:        "  </tbody>\n",
3226:        "</table>\n",
3227:        "<p>2521 rows × 2 columns</p>\n",
3228:        "</div>"
3229:       ],
3230:       "text/plain": [
3231:        "                                                                                                                            review  \\\n",
3232:        "11                                                   great burgers a bit of a too cool for school vibe but overall good experience   \n",
3233:        "28                                                               the best ramen i ve ever had really worth waiting for a long time   \n",
3234:        "87                                                 lively atmosphere great to go with a group of friends the burgers are delicious   \n",
3235:        "93                                   sophies is amazing i can no lt get enough of there empanadas everything in there is delicious   \n",
3236:        "133                  a great japanese place for some japanese fusion cuisine whenever i go here this place never fails to amaze me   \n",
3237:        "...                                                                                                                            ...   \n",
3238:        "49863                                                                 i didnt like it ive tasted much better all bread and no meat   \n",
3239:        "49870                                        great for sunday brunch loved sitting on the outside garden really good eggs benedict   \n",
3240:        "49871  fantastic izakaya extensive sake menu great ambience excellent grilled squid miso rice balls and authentic japanese service   \n",
3241:        "49919                                            absolutely the best coffee in the neighborhood quality sake served with a passion   \n",
3242:        "49944                    ok this is a small place but you will go satisfied very satisfied everything they make is fresh and yummy   \n",
3243:        "\n",
3244:        "       word_count  \n",
3245:        "11             15  \n",
3246:        "28             14  \n",
3247:        "87             14  \n",
3248:        "93             17  \n",
3249:        "133            20  \n",
3250:        "...           ...  \n",
3251:        "49863          13  \n",
3252:        "49870          14  \n",
3253:        "49871          17  \n",
3254:        "49919          13  \n",
3255:        "49944          20  \n",
3256:        "\n",
3257:        "[2521 rows x 2 columns]"
3258:       ]
3259:      },
3260:      "execution_count": 605,
3261:      "metadata": {},
3262:      "output_type": "execute_result"
3263:     }
3264:    ],
3265:    "source": [
3266:     "# AI-generated reviews with 10–20 words\n",
3267:     "ai_reviews_10_20 = yelp_sample[\n",
3268:     "    (yelp_sample[\"label\"] == 1) &\n",
3269:     "    (yelp_sample[\"word_count\"].between(10, 20))\n",
3270:     "]\n",
3271:     "\n",
3272:     "# Display the relevant columns\n",
3273:     "ai_reviews_10_20[[\"review\", \"word_count\"]]"
3274:    ]
3275:   },
3276:   {
3277:    "cell_type": "code",
3278:    "execution_count": 606,
3279:    "id": "487b66a7",
3280:    "metadata": {},
3281:    "outputs": [
3282:     {
3283:      "data": {
3284:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAh0AAAHCCAYAAABL4HuAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAARO5JREFUeJzt3Xl8TXf+x/F39k0WYicEsQSxhCKkTVCttYqWttYZ1c20QzsL03aqNa3+ZjrVxWhNdbRqiX1a2qGoFC1K7BVLtZEIgiBBIuv5/WFyx5WEm7g5N67X8/G4j/Z+z+d87+ckkvvO2a6LYRiGAAAAKpiroxsAAAB3BkIHAAAwBaEDAACYgtABAABMQegAAACmIHQAAABTEDoAAIApCB0AAMAUhA7gNrJixQqtWbPG0W2gEpk3b56+++47R7cB2MSFO5IC//Ptt9/qyJEjGjVqlDw9Pa2WLVu2TOfPn9fQoUMVEBBgtezLL79Uenq6Ro0aVaH9tWvXTrVr19bq1attXicpKUm7d+/WxYsXVadOHTVt2lQNGzaswC7L7tNPP1WzZs0UFRVV5nVvh+2rSNWrV9dDDz2kDz/80NGtADfFng7gGj/88IPGjRunrVu3Wo1nZ2frscce07hx47Ru3TqrZYZhaPTo0frnP/9pZqs3tXv3bkVHR6tly5b6xz/+obVr12ratGlq2rSp7r77biUkJDi6RYvx48dr/vz5ZVrndtq+ijRy5EhFR0c7ug3AJoQO4Bo9evSQJG3YsMFqfPPmzcrNzVV4eLi++eYbq2V79uxRenq6Zd3KYOvWreratauqVKmipKQkrV27VnPnztX69ev1888/y8/PT1u2bHF0m+Xm7NtXFtOnT9eIESMc3QZgE3dHNwBUJu3bt1fVqlX1zTff6JVXXrGMf/PNNwoPD9fQoUO1ePFiq3WKQsj1oePHH3/Unj175Orqqg4dOqhp06ZWy9etW6cLFy7ooYceUlpamjZt2iQfHx/169dPknTp0iVt2LBBly9fVteuXdWgQQObtqGgoEAjR45UzZo1tWzZMvn5+Vktr1+/vlatWqVDhw5Zjefl5WnLli06duyYAgMDFR0drWrVqlmWZ2dna/78+YqKilKrVq2s1l2+fLmqVKmi++67zzL2r3/9S61bt1anTp20d+9e7d27V/Xq1VNMTIxcXa/+vZOTk6PPPvtM+fn5OnDggGbPni1Jqlevnvr06WPq9l3f886dO3Xw4EG1bt1abdq0sdTs2rVLBw4cUOPGjUs8HHTtHAkJCUpMTFSDBg0UHR1t2e5rv27nzp2TJLm7u6tWrVrq1q1bscN31865b98+7dmzR23btlVERITmzZunRo0aqVu3blbr7Nu3T4cOHZKbm5vatm2rxo0bF+u1rF+T0r6PgM0MAFYGDRpkeHp6GllZWZaxTp06Gc8884yxYcMGQ5Jx8uRJy7L+/fsbPj4+xpUrVwzDMIyMjAyjX79+ho+Pj9GnTx+jV69ehqenp/Hoo48a2dnZlvUGDhxoNG/e3FiwYIERERFhDBo0yOjbt69hGIbx3XffGTVr1jQaNGhgPPzww0abNm2Mjz/+2Gjbtq1x//3337D/NWvWGJKMv/zlLzZv886dO43GjRsbderUMR566CGjffv2ho+Pj/H+++9bak6ePGlIMqZPn15s/VatWhn9+vWzGnNzczNeeOEF4ze/+Y0RExNjDBo0yPDz8zOio6ONnJwcwzAM4+LFi8bYsWMNd3d3o2XLlsbYsWONsWPHGn//+99N375rex47dqzRs2dPo3///oa7u7vx6quvGvn5+caYMWOMHj16GAMGDDDc3NyMp556qthrubm5Gc8//7wxZswYIyYmxhg4cKAREBBgdOnSxTh79qxV7Z///GfLNj/22GNGeHi4UaVKFWP58uUl9vX4448bd999t3Hvvfcab731lmEYhhEcHGw8+eSTltrs7GzjvvvuMwIDA41B... (line truncated to 2000 chars)
3285:       "text/plain": [
3286:        "<Figure size 600x500 with 1 Axes>"
3287:       ]
3288:      },
3289:      "metadata": {},
3290:      "output_type": "display_data"
3291:     }
3292:    ],
3293:    "source": [
3294:     "plt.figure(figsize=(6,5))\n",
3295:     "\n",
3296:     "plt.boxplot(\n",
3297:     "    [\n",
3298:     "        amazon_df[amazon_df[\"label\"] == 0][\"word_count\"],\n",
3299:     "        amazon_df[amazon_df[\"label\"] == 1][\"word_count\"]\n",
3300:     "    ],\n",
3301:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
3302:     ")\n",
3303:     "\n",
3304:     "plt.ylabel(\"Word Count\")\n",
3305:     "plt.title(\"Word Count Comparison\")\n",
3306:     "\n",
3307:     "plt.show()"
3308:    ]
3309:   },
3310:   {
3311:    "cell_type": "code",
3312:    "execution_count": 607,
3313:    "id": "b8fb915d",
3314:    "metadata": {},
3315:    "outputs": [
3316:     {
3317:      "data": {
3318:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAiYAAAHCCAYAAADb8wJPAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUEVJREFUeJzt3XlcVPX+P/DXzLCDoLK5sSkaCKhoueDCYm6ooWia5XavqZXde8vqqrdNb92491ZS125pWZrmErnUdV8SChdMScQdIhFBBEQFlJ35/P7gN+fLCOoAh5lh5vV8PObRzPm858x7oHHefM5nUQghBIiIiIiMgNLQCRARERFpsDAhIiIio8HChIiIiIwGCxMiIiIyGixMiIiIyGiwMCEiIiKjwcKEiIiIjAYLEyIiIjIaLEyITMz27duxb98+Q6dBRuSbb77BkSNHDJ0GkU4UXPmVqHF++uknpKenY+bMmbCystJq27p1K27duoUpU6bA0dFRq23Xrl0oLCzEzJkzWzS/Pn36oEOHDti7d6/Oz8nMzERKSgpKSkrQsWNHdO/eHV5eXi2YZeN9/fXX6NGjBwYNGtTo57aG99eSXFxcMHnyZKxcudLQqRA9FHtMiBrpl19+wdy5c5GUlKR1vKysDE8//TTmzp2LgwcParUJITBr1ix8/vnn+kz1oVJSUjBkyBD07NkT//3vf3HgwAHExMSge/fuGDp0KJKTkw2domTBggXYsGFDo57Tmt5fS5oxYwaGDBli6DSIdMLChKiRIiIiAADx8fFaxw8fPozKykr4+/vj0KFDWm2nT59GYWGh9FxjkJSUhJCQEDg4OCAzMxMHDhzAunXr8OOPP+L333+Hvb09jh07Zug0m8zU319jxMbGYvr06YZOg0gnFoZOgKi1CQ4ORrt27XDo0CG8/fbb0vFDhw7B398fU6ZMQVxcnNZzNIXKvYXJuXPncPr0aSiVSvTr1w/du3fXaj948CBu376NyZMnIy8vD4mJibC1tcXYsWMBAHfu3EF8fDzu3r2LkJAQeHp66vQeampqMGPGDLi5uWHr1q2wt7fXau/SpQt27tyJS5cuaR2vqqrCsWPHcOXKFTg5OWHIkCFo37691F5WVoYNGzZg0KBBCAgI0Hrutm3b4ODggJEjR0rHvvrqKwQGBqJ///5ITU1FamoqOnfujNDQUCiVtX83VVRUYP369aiursb58+exevVqAEDnzp0xZswYvb6/e3P+9ddfcfHiRQQGBqJXr15SzKlTp3D+/Hl07dq1wUtPdc+RnJyMCxcuwNPTE0OGDJHed92f282bNwEAFhYWcHd3x+DBg+tdKqx7zjNnzuD06dPo3bs3goKC8M0338DHxweDBw/Wes6ZM2dw6dIlqFQq9O7dG127dq2Xa2N/Jvf7PRLpTBBRo02cOFFYWVmJ0tJS6Vj//v3FCy+8IOLj4wUAkZubK7WNGzdO2NraivLyciGEEEVFRWLs2LHC1tZWjBkzRowYMUJYWVmJadOmibKyMul5UVFR4pFHHhEbN24UQUFBYuLEiSIyMlIIIcSRI0eEm5ub8PT0FE8++aTo1auX+PLLL0Xv3r3FqFGjHpj/vn37BADx7rvv6vyef/31V9G1a1fRsWNHMXnyZBEcHCxsbW3FihUrpJjc3FwBQMTGxtZ7fkBAgBg7dqzWMZVKJV555RXx4osvitDQUDFx4kRhb28vhgwZIioqKoQQQpSUlIg5c+YICwsL0bNnTzFnzhwxZ84c8eGHH+r9/dXNec6cOWL48OFi3LhxwsLCQixbtkxUV1eL2bNni4iICDF+/HihUqnEc889V++1VCqVWLhwoZg9e7YIDQ0VUVFRwtHRUQwcOFDcuHFDK/att96S3vPTTz8t/P39hYODg9i2bVuDeT377LNi6NCh4vHHHxcffPCBEEIIZ2dnMX/+fCm2rKxMjBw5Ujg5OYmJEyeKJ598UvTo0UNMmTKlWT+T... (line truncated to 2000 chars)
3319:       "text/plain": [
3320:        "<Figure size 600x500 with 1 Axes>"
3321:       ]
3322:      },
3323:      "metadata": {},
3324:      "output_type": "display_data"
3325:     }
3326:    ],
3327:    "source": [
3328:     "plt.figure(figsize=(6,5))\n",
3329:     "\n",
3330:     "plt.boxplot(\n",
3331:     "    [\n",
3332:     "        yelp_sample[yelp_sample[\"label\"] == 0][\"word_count\"],\n",
3333:     "        yelp_sample[yelp_sample[\"label\"] == 1][\"word_count\"]\n",
3334:     "    ],\n",
3335:     "    tick_labels=[\"Genuine\", \"AI Generated\"]\n",
3336:     ")\n",
3337:     "\n",
3338:     "plt.ylabel(\"Word Count\")\n",
3339:     "plt.title(\"Word Count Comparison\")\n",
3340:     "\n",
3341:     "plt.show()"
3342:    ]
3343:   },
3344:   {
3345:    "cell_type": "code",
3346:    "execution_count": 608,
3347:    "id": "bf96bddf",
3348:    "metadata": {},
3349:    "outputs": [
3350:     {
3351:      "data": {
3352:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUvVJREFUeJzt3Xd4VGX6xvE7CekVAhhCEnoTqUESxEKXmiCyiygsq4iICijYUBBRabquorurCC4qrrDSOygQEBHpiEiTCCGAgYQ00tv5/cGPWYccIAMTJiHfz3XNdTHvec57npkJeHvyzjlOhmEYAgAAAGDF2dENAAAAAGURQRkAAAAwQVAGAAAATBCUAQAAABMEZQAAAMAEQRkAAAAwQVAGAAAATBCUAQAAABMEZQBAubBu3TotW7bMocdbvny5Vq1addN6uFIfAG4OJ+7MB8CefvnlFx07dky5ubmqX7++WrRoIRcXl1I/7qpVq1RYWKioqKhSP9bNlpSUpJ07dyopKUmBgYGqXbu2br/9dke3ZcXW9z8mJkaxsbGSJCcnJ3l5eSkwMFB33HGHgoODTffp3r27kpKStGvXrlLt7WrHi4yMlIeHhzZt2mTTXDfS4/W+bgA3rpKjGwBwazhy5Igef/xx7d69Wx06dFBAQIC+//57GYahcePG6amnnirV47/zzjvKycm5pYJyQkKCRo0apaVLl6pNmzaqV6+eUlNTtXnzZgUHB2vKlCnq16+fo9uUZPv7P3PmTP33v//VY489JicnJ+Xm5urUqVPasWOHGjdurAkTJqhv375W+3Tv3l0ZGRml3tuNHu96XK3Hm9kHAGsEZQA3zDAMRUVFKSsrS7/++qtq1qwpSSooKNDUqVM1f/78Ug/Kt5qEhAS1bdtWXl5e2rdvn9UZ5IyMDL388stasWJFmQnK12vmzJmqVOl//ylKTU3Vyy+/rAceeEDTp0/Xiy++aNn27LPP3tTebvbxrqSs9AFURARlADfsyJEjOnr0qMaOHWsJyZJUqVIlTZgwQb179zbd7/jx49q1a5fy8vJ0xx13qEWLFlbbly9fLhcXF/Xq1UsnT57U1q1b5evrq06dOsnLy8tS99///le///67CgoKNHv2bEmSu7u7Bg8eXCrH+6OTJ09q586dKiwsVKtWrdSgQQObX6eZkSNHKiEhQb/88kuxOX18fPSPf/xDP/30U7H99uzZo0OHDsnNzU1t27ZVrVq1rLbPmzdPNWrUUIcOHazGv/vuO506dUoPP/ywze9HSd//kggICNDHH3+sEydO6NVXX1W/fv1Uv359SRfX6ubk5Cg6Otpqn7i4OO3bt085OTlq3Lix1ft7rd4uf43btm1T9erV1bFjxyse75LY2Fht375dAQEB6tixozw9Pa22l/S9vlaPV+vjWp/39fxMA/gDAwBu0OnTpw1JxuDBg0tUn5GRYQwcONBwc3MzunbtavTr188ICAgw+vTpY1y4cMFSFxERYdx3333GrFmzjPDwcONPf/qTcdtttxm1atUy4uPjLXUvvfSSERQUZFSrVs0YOnSoMXToUGPkyJGldjzDMIwLFy4YDz/8sOHq6mrcc889xp///GejcePGxsMPP2zzcS+XmJhoODs7G3379i3R+2kYhpGQkGDcfffdhq+vrxEVFWV07NjRqFSpkvHUU08ZBQUFlrqaNWsajzzySLH9hwwZYtx2221WY/Z6/80MGDDAkGTk5+ebbl+5cqUhyXjjjTcsY/fff78RHh5uVffss88anp6eRvfu3Y2HH37YaN26tdG+fXsjISGhRL1deo0ffPCB0apVKyMqKsr4y1/+csXjXar/+9//brRu3dro37+/ERwcbISGhhr79++3qi3pe32tHs36KOnnbcvPNIDiCMoA7KJnz56Gs7OzMWrUKGPbtm1Gdnb2FWsHDhxo+Pj4GHv37rWMxcXFGbfddpsxbNgwy1hERIRRs2ZNY9y4cZax... (line truncated to 2000 chars)
3353:       "text/plain": [
3354:        "<Figure size 800x500 with 1 Axes>"
3355:       ]
3356:      },
3357:      "metadata": {},
3358:      "output_type": "display_data"
3359:     }
3360:    ],
3361:    "source": [
3362:     "plt.figure(figsize=(8,5))\n",
3363:     "\n",
3364:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"sentence_count\"], bins=25, alpha=0.6, label=\"Genuine\")\n",
3365:     "\n",
3366:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"sentence_count\"], bins=25, alpha=0.6, label=\"AI Generated\")\n",
3367:     "\n",
3368:     "plt.title(\"Sentence Count Distribution\")\n",
3369:     "plt.xlabel(\"Sentence Count\")\n",
3370:     "plt.ylabel(\"Frequency\")\n",
3371:     "plt.legend()\n",
3372:     "\n",
3373:     "plt.show()"
3374:    ]
3375:   },
3376:   {
3377:    "cell_type": "code",
3378:    "execution_count": 609,
3379:    "id": "157bae5d",
3380:    "metadata": {},
3381:    "outputs": [
3382:     {
3383:      "data": {
3384:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsoAAAHVCAYAAADo/t2TAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAASKJJREFUeJzt3XlcVXX+x/E3ILssihog4L5lrphgWrnviqmlpeQ4jKWZZpqZoy3OlEvWmE7zK8vJzEon9zSX3DUzt1wyt0QT1FCQTRQQ4fz+aLzTlaNy5cJFfT0fj/t4dL/ne77fzz0H7e3he89xMgzDEAAAAAArzo4uAAAAACiJCMoAAACACYIyAAAAYIKgDAAAAJggKAMAAAAmCMoAAACACYIyAAAAYIKgDAAAAJggKAMA7ghr1qzRsmXLHDrf119/rW+++abYarhRHQCKhxNP5gNgTz///LOOHz+u7OxsVa9eXQ0aNJCLi0uRz/vNN98oNzdX3bt3L/K5iltSUpJ27dqlpKQkBQQEqHLlyrr//vsdXZYVW4//xo0bFRsbK0lycnKSl5eXAgIC9MADDyg4ONh0n44dOyopKUm7d+8u0tpuNl9kZKQ8PDy0adMmm8YqTI23+7kBFF4pRxcA4O5w9OhR/eUvf9GePXvUsmVL+fv767vvvpNhGBo7dqyee+65Ip1/6tSpysrKuquCckJCgoYPH66lS5eqSZMmqlatmlJTU7V582YFBwdr4sSJ6tmzp6PLlGT78Z85c6b+85//6M9//rOcnJyUnZ2t06dPa+fOnapdu7ZeffVV9ejRw2qfjh07KiMjo8hrK+x8t+NmNRZnHQCsEZQBFJphGOrevbsuX76sX375RRUrVpQkXb16VZMmTdL8+fOLPCjfbRISEtS0aVN5eXlp3759VleQMzIy9Morr2j58uUlJijfrpkzZ6pUqf/9ryg1NVWvvPKKHnvsMU2ZMkUvv/yyZduIESOKtbbinu9GSkodwL2IoAyg0I4ePapjx45p1KhRlpAsSaVKldKrr76qrl27mu538uRJ7d69W1euXNEDDzygBg0aWG3/+uuv5eLioi5duiguLk7btm2Tj4+PWrduLS8vL0u///znP/rtt9909epVzZo1S5Lk7u6u6OjoIpnvj+Li4rRr1y7l5uaqUaNGqlGjhs2f08ywYcOUkJCgn3/+Od+YpUuX1vvvv6/9+/fn2+/HH3/U4cOH5ebmpqZNm6pSpUpW2+fNm6egoCC1bNnSqn3Lli06ffq0nnrqKZuPR0GPf0H4+/vrww8/1K+//qpx48apZ8+eql69uqTf1+pmZWUpKirKap9Tp05p3759ysrKUu3ata2O761qu/4zbt++XRUqVFCrVq1uON81sbGx2rFjh/z9/dWqVSt5enpabS/osb5VjTer41bn+3Z+pgH8gQEAhXTmzBlDkhEdHV2g/hkZGcaTTz5puLm5Ge3atTN69uxp+Pv7G926dTMuXrxo6RcREWE8+uijxscff2yEh4cbjz/+uHHfffcZlSpVMuLj4y39xowZYwQGBhrly5c3YmJijJiYGGPYsGFFNp9hGMbFixeNp556ynB1dTUefvhh44knnjBq165tPPXUUzbPe73ExETD2dnZ6NGjR4GOp2EYRkJCgtGiRQvDx8fH6N69u9GqVSujVKlSxnPPPWdcvXrV0q9ixYpGv3798u0/YMAA47777rNqs9fxN9OnTx9DkpGTk2O6fcWKFYYk429/+5ulrUOHDkZ4eLhVvxEjRhienp5Gx44djaeeespo3Lix0bx5cyMhIaFAtV37jDNmzDAaNWpkdO/e3Xj66advON+1/v/4xz+Mxo0bG7179zaCg4ON0NBQ48CBA1Z9C3qsb1WjWR0FPd+2/EwDyI+gDMAuOnfubDg7OxvDhw83tm/fbmRmZt6w75NPPmmULl3a2Lt3r6Xt1KlTxn333WcMGjTI0hYREWFUrFjRGDt2... (line truncated to 2000 chars)
3385:       "text/plain": [
3386:        "<Figure size 800x500 with 1 Axes>"
3387:       ]
3388:      },
3389:      "metadata": {},
3390:      "output_type": "display_data"
3391:     }
3392:    ],
3393:    "source": [
3394:     "plt.figure(figsize=(8,5))\n",
3395:     "\n",
3396:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"sentence_count\"], bins=25, alpha=0.6, label=\"Genuine\")\n",
3397:     "\n",
3398:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"sentence_count\"], bins=25, alpha=0.6, label=\"AI Generated\")\n",
3399:     "\n",
3400:     "plt.title(\"Sentence Count Distribution\")\n",
3401:     "plt.xlabel(\"Sentence Count\")\n",
3402:     "plt.ylabel(\"Frequency\")\n",
3403:     "plt.legend()\n",
3404:     "\n",
3405:     "plt.show()"
3406:    ]
3407:   },
3408:   {
3409:    "cell_type": "code",
3410:    "execution_count": 610,
3411:    "id": "702ddf2b",
3412:    "metadata": {},
3413:    "outputs": [],
3414:    "source": [
3415:     "def vocab_richness(text):\n",
3416:     "    words = text.split()\n",
3417:     "    if len(words) == 0:\n",
3418:     "        return 0\n",
3419:     "    return len(set(words)) / len(words)\n",
3420:     "\n",
3421:     "amazon_df[\"vocab_richness\"] = amazon_df[\"review\"].apply(vocab_richness)"
3422:    ]
3423:   },
3424:   {
3425:    "cell_type": "code",
3426:    "execution_count": 611,
3427:    "id": "c57b8d36",
3428:    "metadata": {},
3429:    "outputs": [
3430:     {
3431:      "data": {
3432:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAATLZJREFUeJzt3Xd4FFX//vF7SSWQRkIJSAkdROkgRUFpQUSaEgQBBRQRFdBHFAvw+Kio2LtSrSC9qICgIkVAEKRJJxBCL4EEElLP7w9+2S9LCruwKWTer+vKdbFnzsx8pqy5nZyZsRljjAAAAAALKZLfBQAAAAB5jRAMAAAAyyEEAwAAwHIIwQAAALAcQjAAAAAshxAMAAAAyyEEAwAAwHIIwQAAALAcQjCAPNekSRONHTvW7ctt06aNRo4c6fbl5qVr3Ybc2qc3qrw+F7JaX34ck8LwHQDyCiEYKGTatGmj9u3b59hn9OjRqlWrlmJiYvKoKke7d+/WsWPH3L7cffv26ciRI25f7vXo1q2batasqZo1a6pWrVqqX7++evTooVmzZmXZ/1q3Ibf2aUFw+T6sXbu2GjdurHvuuUcvvviiNm7cmOU817ofb7/9do0aNcrl+bJaX24dk5xqLIjfAaCg8szvAgC412233abXX39da9asUbNmzTJNT0pK0scff6zatWvrpptuyocKrSUqKkqJiYlasmSJJOnUqVOaMmWK7r//fr300kv63//+59D/119/lZ+fX36UWmBduQ8TEhIUFRWlBQsWqHHjxurRo4emTp3qsN+udT/u2bNHVapUcXm+vDxuOdXI+QM4jxAMFDIDBw7UuHHjNGnSpCxD8OzZsxUbG6tHHnkkH6qzJi8vL9WsWdP+uUWLFtq4caPGjx+vUaNGOYSWawlgVnDlPmzQoIF69Oih+++/X126dJGHh4emTZtmn57X+7GgHLeCUgdwI2A4BFDIVK5cWXfddZd++OEHnT9/PtP0iRMnKiAgQPfff7+9bf78+eratavq1q2rli1basyYMTp79mymedevX6+BAweqcePGatGihZ599lmdOnXKPr1Xr172P1vXqVNHd955p1577TVduHAhy1r37dunvn37qn79+urUqZMWL17sMD0hIUE1a9bU559/nmneXr16qV+/flfdH87WlDF+88CBAxo4cKDq16+vjz/+WN26dVO3bt2yXPagQYPUunVrGWOuWsflbDab6tevr6SkJB08eNBhWnZjOq+27zPExMTY64+IiLBfPc1qW53pK0l//fWX+vfvr4YNG6pRo0YaOnSooqOjHfps3rxZAwcOVLNmzdS8eXMNHjxYO3fudLmPq+655x716tVL06dP1/bt2+3tWe3HnNafnJysmjVr6tSpU5o7d679nOnVq1em/XblOZLd+jK46zx3psbs6nDmO+7qeQHc8AyAQmf69OlGkpk4caJD+759+4zNZjNDhgyxt40ZM8bYbDbz7LPPmjVr1pgffvjBlC9f3lSvXt2cPn3a3m/ChAmmSJEipnfv3mbx4sXmzz//NG+//bbp1KmTvc+BAwfMjh07zI4dO8ymTZvM1KlTTYUKFUyHDh0c6ggMDDT33Xefad26tZk7d65ZtWqVGTRokLHZbOa7776z94uPjzeSzP/+979M29i0aVPTqlUrh7aKFSuaPn36OLRdS02zZ882S5cuNZMnTzYffvihkWQ2btzo0D86Otp4eHiYZ599NqtDYFe3bl1TpUqVTO0dOnQwkszJkyevug3O7PvAwEATGRlpIiIizNy5c82ff/5pevbsaTw8PMzmzZszbauzfSdPnmw8PDzMoEGDzO+//25+//13c88995jQ0FCzd+9eY4wxO3fuNMWKFTP9+vUzK1euNH/99ZeZOHGiueWWW8yFCxec7uPqPsyQcb6/++672e7Hq60/PT3d7Nixw4SGhpquXbvaz5kDBw447LeszpHsjpu7z3Nnasyq... (line truncated to 2000 chars)
3433:       "text/plain": [
3434:        "<Figure size 800x500 with 1 Axes>"
3435:       ]
3436:      },
3437:      "metadata": {},
3438:      "output_type": "display_data"
3439:     }
3440:    ],
3441:    "source": [
3442:     "plt.figure(figsize=(8,5))\n",
3443:     "\n",
3444:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"vocab_richness\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3445:     "\n",
3446:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"vocab_richness\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3447:     "\n",
3448:     "plt.xlabel(\"Vocabulary Richness\")\n",
3449:     "plt.ylabel(\"Frequency\")\n",
3450:     "plt.title(\"Vocabulary Richness Distribution\")\n",
3451:     "plt.legend()\n",
3452:     "\n",
3453:     "plt.show()"
3454:    ]
3455:   },
3456:   {
3457:    "cell_type": "code",
3458:    "execution_count": 612,
3459:    "id": "8982b997",
3460:    "metadata": {},
3461:    "outputs": [],
3462:    "source": [
3463:     "def vocab_richness(text):\n",
3464:     "    words = text.split()\n",
3465:     "    if len(words) == 0:\n",
3466:     "        return 0\n",
3467:     "    return len(set(words)) / len(words)\n",
3468:     "\n",
3469:     "yelp_sample[\"vocab_richness\"] = yelp_sample[\"review\"].apply(vocab_richness)"
3470:    ]
3471:   },
3472:   {
3473:    "cell_type": "code",
3474:    "execution_count": 613,
3475:    "id": "61457883",
3476:    "metadata": {},
3477:    "outputs": [
3478:     {
3479:      "data": {
3480:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsEAAAHVCAYAAAAQHiZkAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAVdJJREFUeJzt3Xd4FdX+/v07PQRIoYUQAoQaiqJUKUrv0pEiAgoo+rWAnWABzzmKYsGuRwFRUZAqTVBAEEJHOUivARJagIQkQAgp6/mDh/1zk8IO2Slk3q/rynXYa9bMfPY4+3CzsvYaF2OMEQAAAGAhrgVdAAAAAJDfCMEAAACwHEIwAAAALIcQDAAAAMshBAMAAMByCMEAAACwHEIwAAAALIcQDAAAAMshBAPId02aNNGECROcftx27drppZdecvpx89Otvoe8uqa3q/y+FzI7X0H8NykKnwEgvxCCgSKmXbt26tixY7Z9Xn/9ddWuXVvR0dH5VJW9AwcO6PTp004/7uHDh3Xy5EmnHzc3evfurbCwMIWFhal27dq6++671bdvX82dOzfT/rf6HvLqmhYG/7yGderUUePGjXX//ffrlVde0V9//ZXpPrd6He+9916Fh4fneL/MzpdX/02yq7EwfgaAwsq9oAsA4Fz33HOP3nrrLW3cuFHNmjXLsD05OVmffvqp6tSpo4oVKxZAhdYSGRmppKQk/frrr5Kkc+fO6ZtvvtEDDzygV199Vf/+97/t+q9atUo+Pj4FUWqhdeM1vHz5siIjI7Vo0SI1btxYffv21fTp0+2u261ex4MHD6patWo53i8//7tlVyP3D+A4QjBQxIwYMUITJ07U1KlTMw3B8+bNU1xcnB599NECqM6aPDw8FBYWZnvdokUL/fXXX3r33XcVHh5uF1puJYBZwY3XsEGDBurbt68eeOAB9ezZU25ubpo5c6Zte35fx8Ly362w1AHcDpgOARQxVatWVdu2bfXTTz/p4sWLGbZPmTJFvr6+euCBB2xtCxcuVK9evVS/fn21bNlS48eP14ULFzLsu3XrVo0YMUKNGzdWixYt9OKLL+rcuXO27QMHDrT92rpevXpq06aN3nzzTV26dCnTWg8fPqwhQ4bo7rvvVrdu3bR8+XK77ZcvX1ZYWJi+/PLLDPsOHDhQQ4cOven1cLSm6/M3jx49qhEjRujuu+/Wp59+qt69e6t3796ZHnvkyJFq3bq1jDE3reOfXFxcdPfddys5OVnHjh2z25bVnM6bXfvroqOjbfV37tzZNnqa2Xt1pK8kbdmyRcOGDVPDhg3VqFEjPfnkkzp+/Lhdnx07dmjEiBFq1qyZmjdvrlGjRmnfvn057pNT999/vwYOHKhZs2Zp9+7dtvbMrmN257969arCwsJ07tw5LViwwHbPDBw4MMN1u/Eeyep81znrPnekxqzqcOQzntP7ArjtGQBFzqxZs4wkM2XKFLv2w4cPGxcXF/PEE0/Y2saPH29cXFzMiy++aDZu3Gh++uknExISYmrWrGnOnz9v6/f1118bV1dX8+CDD5rly5ebDRs2mPfee89069bN1ufo0aNm7969Zu/evWb79u1m+vTpplKlSqZTp052dfj5+Zl+/fqZ1q1bmwULFpiIiAgzcuRI4+LiYn744Qdbv8TERCPJ/Pvf/87wHps2bWpatWpl11a5cmUzePBgu7ZbqWnevHlmxYoVZtq0aebjjz82ksxff/1l1//48ePGzc3NvPjii5n9J7CpX7++qVatWob2Tp06GUnm7NmzN30Pjlx7Pz8/M2DAANO5c2ezYMECs2HDBtO/f3/j5uZmduzYkeG9Otp32rRpxs3NzYwcOdKsXr3arF692tx///2mTJky5tChQ8YYY/bt22eKFy9uhg4datatW2e2bNlipkyZYu644w5z6dIlh/vk9Bped/1+/+CDD7K8jjc7f3p6utm7d68pU6aM6dWrl+2eOXr0qN11y+we... (line truncated to 2000 chars)
3481:       "text/plain": [
3482:        "<Figure size 800x500 with 1 Axes>"
3483:       ]
3484:      },
3485:      "metadata": {},
3486:      "output_type": "display_data"
3487:     }
3488:    ],
3489:    "source": [
3490:     "plt.figure(figsize=(8,5))\n",
3491:     "\n",
3492:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"vocab_richness\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3493:     "\n",
3494:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"vocab_richness\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3495:     "\n",
3496:     "plt.xlabel(\"Vocabulary Richness\")\n",
3497:     "plt.ylabel(\"Frequency\")\n",
3498:     "plt.title(\"Vocabulary Richness Distribution\")\n",
3499:     "plt.legend()\n",
3500:     "\n",
3501:     "plt.show()"
3502:    ]
3503:   },
3504:   {
3505:    "cell_type": "code",
3506:    "execution_count": 614,
3507:    "id": "242b11d8",
3508:    "metadata": {},
3509:    "outputs": [],
3510:    "source": [
3511:     "def avg_word_length(text):\n",
3512:     "    words = text.split()\n",
3513:     "    if len(words) == 0:\n",
3514:     "        return 0\n",
3515:     "    return np.mean([len(word) for word in words])\n",
3516:     "\n",
3517:     "amazon_df[\"avg_word_len\"] = amazon_df[\"review\"].apply(avg_word_length)"
3518:    ]
3519:   },
3520:   {
3521:    "cell_type": "code",
3522:    "execution_count": 615,
3523:    "id": "9adcc1c9",
3524:    "metadata": {},
3525:    "outputs": [
3526:     {
3527:      "data": {
3528:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAq0AAAHVCAYAAADbxcKaAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAR1VJREFUeJzt3XlcVdX+//E3AoKAguI8z+JsDpVTTjlrWuZA2WB6LdPSspuRebWyNLu3W7euWamhpgkpmvNNTU1NU8u5cMp5AkFAQRnX7w9/7K8nUAHRs4XX8/Hg8fCsvfban33Osd4u1t7bxRhjBAAAANhYAWcXAAAAANwKoRUAAAC2R2gFAACA7RFaAQAAYHuEVgAAANgeoRUAAAC2R2gFAACA7RFaAQAAYHuEVgDIoSlTpqhevXrOLuOOSk1NVUBAgD755JO7etwmTZpo0qRJTjtefjlv4F5CaAVs4Mcff1RAQIBatGihtLQ0Z5djG2vXrlVAQIAWLlyYYVtQUJACAgI0ffr0DNumTJmigIAAHT169I7WFxERofDw8Fv2mzBhggICAhQTE3NH67kd9erV05QpUzK0G2N04MABRUZG5njstm3bKiAgQAEBAapTp47uv/9+PfLII5owYYJ+//33TPc5cOCAzp8/n+1j3eg8buWvx8uN876Rm9WY0/MG8gM3ZxcAQPr888915swZHThwQKtWrVK3bt2cXZItNGzYUAcPHtSyZcvUp08fh22hoaE6ceKEFi9erCFDhjhsCwsL08WLF1W5cuW7WO2NnTt3TgcOHFBKSoqzS7mh8PBwRURE3JGxDx8+rOLFi2v+/PmSpMuXL+vIkSNasGCB6tWrp8GDB2vq1Klyd3e39vntt9/k5+eX7WPl9DxyerycuFmNd7MO4F5DaAWcLDIyUt9//73ef/99ff311/rqq68Irf9f8eLFVb9+ff34448O7SdOnNCff/6pwYMHKzQ0VCkpKXJzu/afs0uXLunXX39Vnz595OLi4oyykQlPT08FBARYr5s2bar+/ftr9uzZeuaZZ+Tp6alPP/3U2l6zZs27Wt/dPt6N2KUOwI5YHgA4WXBwsFxdXTVo0CANGzZMy5Yt07lz56ztq1evVkBAgNatW5dh37179yogIEChoaFWW0JCgv71r3+pQ4cOatCggbp06aLZs2c77Dd79mwFBATowoULmjlzptq1a6fatWtLkjZt2mT9Krd27dpq3LixBg4cqE2bNmU4/p9//qnnnntO9913nzp27KilS5dqy5YtCggI0JYtWxz6ZqWuzLRv394KqenWrl2rQoUKacyYMbp06ZJ27Nhhbfvpp5+UkpKi9u3bW22RkZEKCgpSixYt1KhRIz3++OP64YcfHI4zd+5cBQQE6Pz58woODlb79u1Vu3ZtpaamWsfs2bOnGjVqpMDAwCwtC8iu9evX64knntB9992n+++/X6NHj3b4VfH16ywPHz6sgQMHqlGjRurRo4c2b96cYbzU1FR98sknat26tZo1a6bXX39d8fHx6tatm0aMGCFJOn/+vAICApSamqqvv/7a+uyHDRuWYbysHDO7nn76aXXq1EnTpk3TmTNnrPbM1nZu3bpVTz31lB544AG1bt1aL730ko4dO5al87j+vQsPD9fAgQPVsGFDzZ0794bHS7d//371799fjRo1Uu/evbVx40aH7adPn1ZAQIBCQkIy7Nu5c2eNHDkySzXerI558+apR48eatCggdq0aaNJkyYpPj7e2p7d7wZwTzIAnKpWrVrm6aefNsYYExsba3x8fMykSZOs7VeuXDFFixY1/fv3z7Dvyy+/bDw8PExUVJS1f6NGjUzFihXNrFmzzPbt283nn39uihQpYkaNGmXt9+9//9tIMiNHjjR///vfzebNm83o0aONMcZcvnzZ/PHHH+aPP/4wv//+u1m/fr0ZPHiwKVCggNm4caM1xtGjR03x4sVNkyZNzPLly81P... (line truncated to 2000 chars)
3529:       "text/plain": [
3530:        "<Figure size 800x500 with 1 Axes>"
3531:       ]
3532:      },
3533:      "metadata": {},
3534:      "output_type": "display_data"
3535:     }
3536:    ],
3537:    "source": [
3538:     "plt.figure(figsize=(8,5))\n",
3539:     "\n",
3540:     "plt.hist(amazon_df[amazon_df[\"label\"] == 0][\"avg_word_len\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3541:     "\n",
3542:     "plt.hist(amazon_df[amazon_df[\"label\"] == 1][\"avg_word_len\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3543:     "\n",
3544:     "plt.title(\"Average Word Length Distribution\")\n",
3545:     "plt.xlabel(\"Average Word Length\")\n",
3546:     "plt.legend()\n",
3547:     "\n",
3548:     "plt.show()"
3549:    ]
3550:   },
3551:   {
3552:    "cell_type": "code",
3553:    "execution_count": 616,
3554:    "id": "cdc4b080",
3555:    "metadata": {},
3556:    "outputs": [],
3557:    "source": [
3558:     "def avg_word_length(text):\n",
3559:     "    words = text.split()\n",
3560:     "    if len(words) == 0:\n",
3561:     "        return 0\n",
3562:     "    return np.mean([len(word) for word in words])\n",
3563:     "\n",
3564:     "yelp_sample[\"avg_word_len\"] = yelp_sample[\"review\"].apply(avg_word_length)"
3565:    ]
3566:   },
3567:   {
3568:    "cell_type": "code",
3569:    "execution_count": 617,
3570:    "id": "57253df7",
3571:    "metadata": {},
3572:    "outputs": [
3573:     {
3574:      "data": {
3575:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArYAAAHVCAYAAAAEi7iFAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAUdxJREFUeJzt3Xt8z/X///H7zGyMjc0w50MYOeRYTs0hZ6KIVjo4pANF6UBS+pSWdPLp9KmQUjJJzioJmZxDiJEcZsxmm23Mzs/fH35eX+82bPNm22u36+Xyvlx6P1+P1+v1eL3f7+W+156v19vFGGMEAAAAFHLF8rsBAAAAwBkItgAAALAFgi0AAABsgWALAAAAWyDYAgAAwBYItgAAALAFgi0AAABsgWALAAAAWyDYAsB19NZbb6lRo0b53cZ1lZGRoYCAAE2fPv2G7rdFixYKDg7Ot/0VleMGChOCLVBI/PrrrwoICFDbtm2VmZmZ3+0UGKtXr1ZAQIC+//77LMsmTJiggIAAzZgxI8uyt956SwEBATp8+PB17S8qKkr79++/at3kyZMVEBCgM2fOXNd+rkWjRo301ltvZRk3xigsLEzR0dF53nbHjh0VEBCggIAANWzYUK1bt9add96pyZMn66+//sp2nbCwMJ06dSrX+7rccVzNv/fnjOO+nCv1mNfjBoqC4vndAICc+eSTT3TixAmFhYXpxx9/VK9evfK7pQKhadOmOnDggJYtW6YBAwY4LJs/f76OHTumRYsWacSIEQ7LFi5cqLi4ONWsWfMGdnt5kZGRCgsLU3p6en63cln79+9XVFTUddn233//rfLly2vevHmSpLNnz+rQoUNasGCBGjVqpOHDh+vjjz+Wm5ubtc4ff/yhsmXL5npfeT2OvO4vL67U443sAyhsCLZAIRAdHa3FixfrjTfe0BdffKHPP/+cYPv/lS9fXo0bN9avv/7qMH7s2DH9888/Gj58uObPn6/09HQVL37hf3mJiYnavn27BgwYIBcXl/xoG9nw8PBQQECA9bxly5YaPHiwvvrqKz300EPy8PDQBx98YC2vV6/eDe3vRu/vcgpKH0BBxFQEoBCYPXu2XF1dNXToUD3++ONatmyZIiMjreWrVq1SQECA1qxZk2Xd3bt3KyAgQPPnz7fGkpKS9M4776hLly5q0qSJevTooa+++sphva+++koBAQE6ffq0Zs2apU6dOqlBgwaSpNDQUOvPxg0aNFDz5s01ZMgQhYaGZtn/P//8o2HDhqlZs2bq2rWrli5dqo0bNyogIEAbN250qM1JX9np3LmzFWQvWr16tUqWLKkXXnhBiYmJ2rZtm7Xst99+U3p6ujp37myNRUdHa8KECWrbtq1uueUWDRw4UD///LPDfr755hsFBATo1KlTmj17tjp37qwGDRooIyPD2mffvn11yy23KCgoKEdTEHJr7dq1uu+++9SsWTO1bt1a48aNc/iz9KXzPv/++28NGTJEt9xyi/r06aMNGzZk2V5GRoamT5+uDh06qFWrVnr++ed17tw59erVS6NHj5YknTp1SgEBAcrIyNAXX3xhvfePP/54lu3lZJ+59eCDD6pbt2763//+pxMnTljj2c013bRpkx544AHdeuut6tChg5588kkdOXIkR8dx6Wu3f/9+DRkyRE2bNtU333xz2f1dtHfvXg0ePFi33HKL+vfvr/Xr1zssj4iIUEBAgEJCQrKs2717d40ZMyZHPV6pj7lz56pPnz5q0qSJAgMDFRwcrHPnzlnLc/vZAAolA6DAq1+/vnnwwQeNMcbEx8eb0qVLm+DgYGv5+fPnTbly5czgwYOzrPvUU08Zd3d3ExMTY61/yy23mOrVq5svv/zSbN261XzyySfGy8vLjB071lrvvffeM5LMmDFjzHPPPWc2bNhgxo0bZ4wx5uzZs2bfvn1m37595q+//jJr1641w4cPN8WKFTPr16+3tnH48GFTvnx5... (line truncated to 2000 chars)
3576:       "text/plain": [
3577:        "<Figure size 800x500 with 1 Axes>"
3578:       ]
3579:      },
3580:      "metadata": {},
3581:      "output_type": "display_data"
3582:     }
3583:    ],
3584:    "source": [
3585:     "plt.figure(figsize=(8,5))\n",
3586:     "\n",
3587:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 0][\"avg_word_len\"], bins=30, alpha=0.6, label=\"Genuine\")\n",
3588:     "\n",
3589:     "plt.hist(yelp_sample[yelp_sample[\"label\"] == 1][\"avg_word_len\"], bins=30, alpha=0.6, label=\"AI Generated\")\n",
3590:     "\n",
3591:     "plt.title(\"Average Word Length Distribution\")\n",
3592:     "plt.xlabel(\"Average Word Length\")\n",
3593:     "plt.legend()\n",
3594:     "\n",
3595:     "plt.show()"
3596:    ]
3597:   },
3598:   {
3599:    "cell_type": "code",
3600:    "execution_count": 618,
3601:    "id": "e5c984ac",
3602:    "metadata": {},
3603:    "outputs": [
3604:     {
3605:      "data": {

(Output capped at 50 KB. Showing lines 2788-3605. Use offset=3606 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 5.4s)

_Thinking:_

Let me continue reading to see the rest of the notebook.

**Tool: read**

**Input:**
```json
{
  "filePath": "/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb",
  "offset": 3606
}
```

**Output:**
```
<path>/home/hitesh/Data/Work/Projects/Cross-Domain-Fake-Review-Detection/cross-domain-V2.ipynb</path>
<type>file</type>
<content>
3606:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXd8HGed+P+esr1Jq94tWS5y7yV2ilt6IyEmoRyBEODgaAe/y93BHeTgS79QA8eFNAghIb0X23ES996bLFu9t9Vq+87M8/tjJdmyZFuSJTvh9s1LxDv7zPM8M/vMM8/n+TRJCCFIkiRJkiRJkiRJkiRJkgtAvtQdSJIkSZIkSZIkSZIkyYefpGCRJEmSJEmSJEmSJEmSCyYpWCRJkiRJkiRJkiRJkuSCSQoWSZIkSZIkSZIkSZIkuWCSgkWSJEmSJEmSJEmSJEkumKRgkSRJkiRJkiRJkiRJkgsmKVgkSZIkSZIkSZIkSZLkgkkKFkmSJEmSJEmSJEmSJLlgkoJFkiRJPtTous6zzz7L0aNHR7Xe7u5unn32WWpqaka13qEyVtf1YeNS/w6XkldffZVdu3Zd6m4kSZIkyZCRkpm3kyRJcj7eeOMNVFVl1apV/Y5rmsaLL76IzWbjhhtuGHDe888/T2ZmJkuXLh2zvgUCAVwuF9///vf5zne+M+TzqqurKS8vJx6PU1BQwPjx47Hb7X3fHz16lLKyMv785z/zyU9+ciy6fk5Gel3DoaGhgSNHjhAOh8nOzqaoqIiMjIwxaWukXMrfIRqN8sorr/R9liQJt9vNtGnTyMnJGfP2s7OzufHGG/njH/845m0lSZIkyWigXuoOJEmS5IPPb3/7W9avX09nZycWi6Xv+LZt27jjjjuQJInW1lbS0tL6visvL+f222/nm9/85pgKFsNlzZo13HfffRw7doz58+fjdDo5duwYjY2N3HXXXfz0pz8lNTX1UndzTFm/fj333XcfBw8eZM6cOXi9XhoaGtizZw+LFy/mW9/6Frfeeuul7iYAbreb22+/naKioovedmdnJ3fccQfjx49n1qxZCCGorKxk7969rF69mkcffRSbzTZm7d90003MnTt3zOpPkiRJktEmaQqVJEmS87J8+XLC4TBbt27td/ydd94hPz8fs9nM+vXrB3zXe+4Hhccff5xrr72WefPm0djYyLvvvsurr77K8ePHef7553nrrbeorq6+1N0cU5544glWrlzJ7NmzaWhoYOPGjbz88svs3LmTyspKcnJyeOyxxy51N/vIzc3l2Wef5fLLL79kfbj22mt59tlnee6559i9eze/+93vePrpp7n//vvHtN2HHnqIL37xi2PaRpIkSZKMJknBIkmSJOelVzgYTHhYtWoVixYt6hMkelm/fj2qqnLFFVf0O37o0CFeeeUV3n33XQKBwIC2XnnllT678vr6el577TUOHTrU931XVxdvvfUW69evJxqNDvka6uvr+eIXv8jKlSv53//9X9xud7/vr776ajZu3DgkU6BYLMbmzZt5+eWX2bVrF7quD2jr2WefpbOzs9/xeDzOs88+y7FjxwbUOdLrGg719fXce++9XHvttfzhD38gJSWl3/eFhYU888wzfOMb3xhwrhCC/fv388orr/D+++8TiUT6fd/R0cGzzz5LQ0MDAHv37uXVV1+lsrJy0H4M9f4M5mMxnLaG2v/h8MUvfhGn08mrr7466PfV1dW8/vrrvPXWW7S1tfX77sUXXxwgoPeyY8cOXnzxxb7P5/KxOFcb7733Hu+++26/Y4cOHeLZZ5+lqqqq3/HXXnuNnTt39jtWU1PD2rVrWb9+PS0tLYO2nyRJkiSDIpIkSZLkPBiGIdLS0sTll1/edywcDguLxSL+9Kc/ie9+97ti0qRJ/cpnZmaKyy67rO9YZWWlWLBggXC5XGL58uVi0qRJwuVyid/97nf92kpLSxP33HOPuP/++8W0adPE... (line truncated to 2000 chars)
3607:       "text/plain": [
3608:        "<Figure size 1000x500 with 1 Axes>"
3609:       ]
3610:      },
3611:      "metadata": {},
3612:      "output_type": "display_data"
3613:     }
3614:    ],
3615:    "source": [
3616:     "genuine_text = \" \".join(amazon_df[amazon_df[\"label\"] == 0][\"review\"])\n",
3617:     "\n",
3618:     "wordcloud = WordCloud(\n",
3619:     "    width=800,\n",
3620:     "    height=400,\n",
3621:     "    background_color=\"white\"\n",
3622:     ").generate(genuine_text)\n",
3623:     "\n",
3624:     "plt.figure(figsize=(10,5))\n",
3625:     "plt.imshow(wordcloud)\n",
3626:     "plt.axis(\"off\")\n",
3627:     "plt.title(\"Word Cloud - Genuine Reviews\")\n",
3628:     "plt.show()"
3629:    ]
3630:   },
3631:   {
3632:    "cell_type": "code",
3633:    "execution_count": 619,
3634:    "id": "8a4b1b2d",
3635:    "metadata": {},
3636:    "outputs": [
3637:     {
3638:      "data": {
3639:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsnXd8HOWduJ8p27tWvcuWJffeAWMwpncCIQl3SS7hklwuuVxNLncXksuVXy65lLuUS7gULrTQAoQSMBgMBmPce5Vk9a7V9jYz7++PldYWkmzJlsGQffIx0c68+877zszOvN8uCSEEOXLkyJEjR44cOXLkyHEOyO/1AHLkyJEjR44cOXLkyPH+JydY5MiRI0eOHDly5MiR45zJCRY5cuTIkSNHjhw5cuQ4Z3KCRY4cOXLkyJEjR44cOc6ZnGCRI0eOHDly5MiRI0eOcyYnWOTIkSNHjhw5cuTIkeOcyQkWOXLkyJEjR44cOXLkOGdygkWOHDly5MiRI0eOHDnOmZxgkSNHjncVXdd57LHHOHz48JT2Gw6Heeyxx2hpaZnSfifK+ZpXjguf98u1f+aZZ9ixY8d7PYwcOXJ8gMkJFjlyfAB5/vnn2bBhw6jtmqbx2GOP8eyzz475vSeeeILNmzef17HF43Fuv/12HnvssUl9r7m5mQ0bNvDcc8+xb98+YrHYiP3t7e3cfvvtvPbaa1M53AlztvOaDL/97W957LHHSKfTY+5PJpM89thj7N69e1L9dnR08PLLL/PMM8+wfft2ent7p2C0FxbBYJDHHnuMtra2Ke97otd++PoM/3v88cfZsGEDnZ2dUz6msfj0pz/NT37yk3flWDly5PjDJCdY5MjxAeSHP/whN910E8lkcsT2rVu3cvvtt3PDDTfQ398/Yt/Ro0e57bbbePLJJ9/FkZ6ZDRs2sHjxYmbPns2//uu/8uMf/5hbb72VwsJC7r77bgKBwHs9xHeFzZs3c+utt3L77bfz9NNPj9kmEAhw++2387//+78T6vOVV15h+fLl1NbWcs899/Czn/2Mz372sxQXF3PxxRdfcPfCudDU1MTtt99+3gXn0zF8fb7yla/w8MMP8+CDD/LlL3+ZsrIy7rzzTuLx+Hk9/g033MDSpUvP6zFy5Mjxh01OsMiR4wPI5ZdfTjwe56233hqxfePGjZSXl2M2m3nllVdG7Rv+7oXCfffdx9VXX83SpUvp7Ozk1Vdf5ZlnnuHYsWM88cQTvPDCCzQ3N7/Xw3xX+N///V/Ky8uZP3/+hAWH03H//fdzxRVXsGjRIjo6Oti8eTNPP/0027dvp6mpiZKSEn71q1+d+8BzjOLqq6/OWix27tzJj3/8Y37zm9/wjW9847we99577+Wzn/3seT1Gjhw5/rBR3+sB5MiRY+oZFg5eeeUVLr300uz2jRs3sn79ehobG9m4cSMf+tCHsvteeeUVVFVlzZo1I/o6cOAAjY2NuFwuli5ditPpHLH/d7/7HaWlpSxZsoT29nZ2795NdXU1c+bMATIuKG+99RZms5nVq1dPeA7t7e189rOf5YorruBnP/vZqP1XXnklmzdvRlGUM/aVSqXYvn07fX19lJWVsXDhwhHfa29vZ8uWLaxbtw6fz5fdnk6neeqpp5g3bx719fUj+jzbeZ0NwWCQRx99lK985SsUFRXxuc99jpaWFiorK8+qv/b2du6++26uvvpqfvrTn47aX1lZyaOPPsqmTZtG7RNCsG/fPpqbm/F4PCxfvhyr1ZrdPzAwwMaNG1m9ejWlpaXs3r2btrY25syZQ01NzZjjmWyfe/bsoampiTVr1uByuXjqqaeybS0WC1VVVcybNw9JkoCMq9dLL70EZKx2qpp59c2ePZvZs2dPeBzDTPW1/+xnP8vf/u3f8swzz/D//t//G7W/ubmZAwcOoCgKS5YsIT8/P7vvySefpLi4mJUrV4763rZt22hvb+fmm28GMjEWJSUl... (line truncated to 2000 chars)
3640:       "text/plain": [
3641:        "<Figure size 1000x500 with 1 Axes>"
3642:       ]
3643:      },
3644:      "metadata": {},
3645:      "output_type": "display_data"
3646:     }
3647:    ],
3648:    "source": [
3649:     "fake_text = \" \".join(amazon_df[amazon_df[\"label\"] == 1][\"review\"])\n",
3650:     "\n",
3651:     "wordcloud = WordCloud(\n",
3652:     "    width=800,\n",
3653:     "    height=400,\n",
3654:     "    background_color=\"white\"\n",
3655:     ").generate(fake_text)\n",
3656:     "\n",
3657:     "plt.figure(figsize=(10,5))\n",
3658:     "plt.imshow(wordcloud)\n",
3659:     "plt.axis(\"off\")\n",
3660:     "plt.title(\"Word Cloud - AI Generated Reviews\")\n",
3661:     "plt.show()"
3662:    ]
3663:   },
3664:   {
3665:    "cell_type": "code",
3666:    "execution_count": 620,
3667:    "id": "2b412c33",
3668:    "metadata": {},
3669:    "outputs": [
3670:     {
3671:      "data": {
3672:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsvXecHFeZqP1UVec8oSdHzYw0yjk5yHKQE7ZxwAZjsmHhLvEue4FluWtzYWGBhV0+wsJ6DRhMtGycg2RLlmUr56yRZjQ5T/f0dO6uqvP90TMttWYk9SjY8m4/v5+t6VNVJ3V11fue8wZJCCHIkSNHjhw5cuTIkSNHjgtAfqc7kCNHjhw5cuTIkSNHjnc/OcUiR44cOXLkyJEjR44cF0xOsciRI0eOHDly5MiRI8cFk1MscuTIkSNHjhw5cuTIccHkFIscOXLkyJEjR44cOXJcMDnFIkeOHDly5MiRI0eOHBdMTrHIkSNHjhw5cuTIkSPHBZNTLHLkyJEjR44cOXLkyHHB5BSLHDlyvKvRNI3Vq1dz5MiRi1pvMBhk9erVtLe3X9R6s+VSjevdxjv9PbyTPP/88+zcufOd7kaOHDlyZI2Uy7ydI0eOc/HSSy9hMBhYtWpVRrmqqjz99NNYrVbe8573jLvuqaeeoqioiKuuuuqS9S0UCuF0OvnWt77FN77xjayva2tro6mpiWQySWVlJXV1ddhstvTxI0eOMH36dH73u9/xoQ996FJ0/ayc77gmQ3d3N4cPHyYajVJSUkJ1dTVer/eStHW+vJPfQzwe57nnnkt/liQJl8vFrFmzKC0tveTtl5SUcNttt/Ff//Vfl7ytHDly5LgYGN7pDuTIkePy56c//Snr16/H7/djNpvT5Vu3buXee+9FkiQGBgYoKChIH2tqauKee+7hy1/+8iVVLCbL2rVr+epXv8rRo0dZvHgxDoeDo0eP0tPTw/3338/3v/998vLy3uluXlLWr1/PV7/6VQ4cOMCCBQvIz8+nu7ub3bt3s3z5cv7+7/+eO++8853uJgAul4t77rmH6urqt71tv9/PvffeS11dHfPmzUMIwYkTJ9izZw/33Xcfv/71r7FarZes/dtvv52FCxdesvpz5MiR42KTM4XKkSPHObnuuuuIRqNs2bIlo3zdunVUVFRgMplYv379uGNj114uPPbYY9x8880sWrSInp4eXn/9dZ5//nmOHTvGU089xSuvvEJbW9s73c1LyuOPP84NN9zA/Pnz6e7u5s033+TZZ59lx44dnDhxgtLSUn7zm9+8091MU1ZWxurVq7n66qvfsT7cfPPNrF69mieffJJdu3bx85//nD//+c9885vfvKTtPvLII3zmM5+5pG3kyJEjx8Ukp1jkyJHjnIwpBxMpD6tWrWLZsmVpRWKM9evXYzAYWLFiRUb5wYMHee6553j99dcJhULj2nruuefSduVdXV288MILHDx4MH08EAjwyiuvsH79euLxeNZj6Orq4jOf+Qw33HAD//mf/4nL5co4fuONN/Lmm29mZQqUSCTYtGkTzz77LDt37kTTtHFtrV69Gr/fn1GeTCZZvXo1R48eHVfn+Y5rMnR1dfGpT32Km2++mV/+8pd4PJ6M41VVVTzxxBP87//9v8ddK4Rg3759PPfcc7zxxhvEYrGM4z6fj9WrV9Pd3Q3Anj17eP755zlx4sSE/ch2fibysZhMW9n2fzJ85jOfweFw8Pzzz094vK2tjRdffJFXXnmFwcHBjGNPP/30OAV9jO3bt/P000+nP5/Nx+JsbWzYsIHXX389o+zgwYOsXr2a1tbWjPIXXniBHTt2ZJS1t7fz6quvsn79evr7+ydsP0eOHDkmROTIkSPHOdB1XRQUFIirr746XRaNRoXZbBa//e1vxUMPPSSmTZuWcX5RUZG44oor0mUnTpwQS5YsEU6nU1x33XVi2rRpwul0ip///OcZbRUUFIgHH3xQfPOb... (line truncated to 2000 chars)
3673:       "text/plain": [
3674:        "<Figure size 1000x500 with 1 Axes>"
3675:       ]
3676:      },
3677:      "metadata": {},
3678:      "output_type": "display_data"
3679:     }
3680:    ],
3681:    "source": [
3682:     "genuine_text = \" \".join(yelp_sample[yelp_sample[\"label\"] == 0][\"review\"])\n",
3683:     "\n",
3684:     "wordcloud = WordCloud(\n",
3685:     "    width=800,\n",
3686:     "    height=400,\n",
3687:     "    background_color=\"white\"\n",
3688:     ").generate(genuine_text)\n",
3689:     "\n",
3690:     "plt.figure(figsize=(10,5))\n",
3691:     "plt.imshow(wordcloud)\n",
3692:     "plt.axis(\"off\")\n",
3693:     "plt.title(\"Word Cloud - Genuine Reviews\")\n",
3694:     "plt.show()"
3695:    ]
3696:   },
3697:   {
3698:    "cell_type": "code",
3699:    "execution_count": 621,
3700:    "id": "8e53a10b",
3701:    "metadata": {},
3702:    "outputs": [
3703:     {
3704:      "data": {
3705:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAxYAAAGqCAYAAACWKdKAAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQABAABJREFUeJzsnXd8HNW5sJ8p24t6r5Yly70XsI0LtsH0akpCAgmQkEKSW5Jwc3MDhNRLGt9NhUAg9I4B0wwuYHDv3bItq/eyK22fmfP9sdLaa8m25AI22ef3ky2dmTll6nnP2yQhhCBBggQJEiRIkCBBggQJTgH5s+5AggQJEiRIkCBBggQJzn0SgkWCBAkSJEiQIEGCBAlOmYRgkSBBggQJEiRIkCBBglMmIVgkSJAgQYIECRIkSJDglEkIFgkSJEiQIEGCBAkSJDhlEoJFggQJEiRIkCBBggQJTpmEYJEgQYIECRIkSJAgQYJTJiFYJEiQIEGCBAkSJEiQ4JRJCBYJEiT4VNF1nZdeeok9e/ac1nq7urp46aWXqK6uPq31DpQzNa4EZz/nyrV/88032bhx42fdjQQJEnyOSQgWCRJ8Dnn77bdZunRpn3JN03jppZdYsmRJv8e98sorrFq16oz2LRAIsGjRIl566aVBHVdVVcXSpUt566232L59O36/P257XV0dixYt4sMPPzyd3R0wJzuuwfDqq6/y0ksvEYlE+t0eCoV46aWX2LJly6Dqra+v54MPPuDNN99kw4YNtLS0nIbenl14PB5eeuklamtrT3vdA732vden9+fll19m6dKlNDQ0nPY+9ccdd9zBX/7yl0+lrQQJEvxrkhAsEiT4HPLHP/6Rq666ilAoFFe+du1aFi1axBVXXEFbW1vctn379nHdddfx2muvfYo9PTFLly5l4sSJjBw5kp///Of8+c9/5tprryUzM5M777yTjo6Oz7qLnwqrVq3i2muvZdGiRbz++uv97tPR0cGiRYv4+9//PqA6ly9fztSpUyktLeXee+/l4Ycf5q677iI7O5uZM2eedffCqVBZWcmiRYvOuOB8PHqvzz333MNzzz3HM888ww9/+EPy8vK46aabCAQCZ7T9K664gsmTJ5/RNhIkSPCvTUKwSJDgc8iFF15IIBBgzZo1ceXLli0jPz8fs9nM8uXL+2zrPfZs4YknnmDhwoVMnjyZhoYGVqxYwZtvvklFRQWvvPIK7777LlVVVZ91Nz8V/v73v5Ofn8/YsWMHLDgcj6eeeor58+czYcIE6uvrWbVqFa+//jobNmygsrKSnJwcHn/88VPveII+LFy4MKax2LRpE3/+8595/vnnuf/++89ou4888gh33XXXGW0jQYIE/9qon3UHEiRIcPrpFQ6WL1/O7NmzY+XLli1jwYIFHDx4kGXLlnH99dfHti1fvhxVVZk1a1ZcXTt37uTgwYO4XC4mT56M0+mM2/7GG2+Qm5vLpEmTqKurY8uWLRQXFzNq1CggaoKyZs0azGYz06dPH/AY6urquOuuu5g/fz4PP/xwn+0XXXQRq1atQlGUE9YVDofZsGEDra2t5OXlMX78+Ljj6urqWL16NfPmzSMlJSVWHolEWLx4MWPGjKG8vDyuzpMd18ng8Xh48cUXueeee8jKyuIb3/gG1dXVFBYWnlR9dXV13HnnnSxcuJC//e1vfbYXFhby4osvsnLlyj7bhBBs376dqqoqkpKSmDp1KlarNba9vb2dZcuWMX36dHJzc9myZQu1tbWMGjWKIUOG9Nufwda5detWKisrmTVrFi6Xi8WLF8f2tVgsFBUVMWbMGCRJAqKmXu+//z4Q1dqpavTTN3LkSEaOHDngfvRyuq/9XXfdxfe//33efPNNfvWrX/XZXlVVxc6dO1EUhUmTJpGenh7b9tprr5Gdnc15553X57j169dTV1fH1VdfDUR9LHJycpg0adKg2li5ciVCCObMmRMr27lzJ7t3... (line truncated to 2000 chars)
3706:       "text/plain": [
3707:        "<Figure size 1000x500 with 1 Axes>"
3708:       ]
3709:      },
3710:      "metadata": {},
3711:      "output_type": "display_data"
3712:     }
3713:    ],
3714:    "source": [
3715:     "fake_text = \" \".join(yelp_sample[yelp_sample[\"label\"] == 1][\"review\"])\n",
3716:     "\n",
3717:     "wordcloud = WordCloud(\n",
3718:     "    width=800,\n",
3719:     "    height=400,\n",
3720:     "    background_color=\"white\"\n",
3721:     ").generate(fake_text)\n",
3722:     "\n",
3723:     "plt.figure(figsize=(10,5))\n",
3724:     "plt.imshow(wordcloud)\n",
3725:     "plt.axis(\"off\")\n",
3726:     "plt.title(\"Word Cloud - AI Generated Reviews\")\n",
3727:     "plt.show()"
3728:    ]
3729:   },
3730:   {
3731:    "cell_type": "code",
3732:    "execution_count": 622,
3733:    "id": "9e4c4ec4",
3734:    "metadata": {},
3735:    "outputs": [],
3736:    "source": [
3737:     "def plot_top_words(dataframe, label, title):\n",
3738:     "    vectorizer = CountVectorizer(stop_words=\"english\", max_features=20)\n",
3739:     "\n",
3740:     "    X = vectorizer.fit_transform(dataframe[dataframe[\"label\"] == label][\"review\"])\n",
3741:     "\n",
3742:     "    counts = np.asarray(X.sum(axis=0)).flatten()\n",
3743:     "\n",
3744:     "    words = vectorizer.get_feature_names_out()\n",
3745:     "\n",
3746:     "    pairs = sorted(zip(words, counts), key=lambda x: x[1], reverse=True)\n",
3747:     "\n",
3748:     "    words, counts = zip(*pairs)\n",
3749:     "\n",
3750:     "    plt.figure(figsize=(8,6))\n",
3751:     "    plt.barh(words, counts)\n",
3752:     "    plt.title(title)\n",
3753:     "    plt.xlabel(\"Frequency\")\n",
3754:     "    plt.gca().invert_yaxis()\n",
3755:     "    plt.show()"
3756:    ]
3757:   },
3758:   {
3759:    "cell_type": "code",
3760:    "execution_count": 623,
3761:    "id": "ae6776f1",
3762:    "metadata": {},
3763:    "outputs": [
3764:     {
3765:      "data": {
3766:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAsYAAAIiCAYAAADLvQ4hAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAdHhJREFUeJzt3XdUVEfDBvCHpSxFutJkRQVF7LGBHSsaLCjGbixYYkk0MeYNxhJLgulqEhONXTFGjQK2WMGosceuqIAURQ0i7ALK0ub7g48bN6ABA+wCz++cPcc7d+7M3MXyZDJ3rp4QQoCIiIiIqIqTaXsARERERES6gMGYiIiIiAgMxkREREREABiMiYiIiIgAMBgTEREREQFgMCYiIiIiAsBgTEREREQEgMGYiIiIiAgAgzERUanLycnB6tWrcenSpf/cllKpxOrVqxEdHf3fB1aBVeXvYcuWLThx4oS2h0FUJejxzXdEFd/BgwcRHx//r/Xs7OzQr1+/Mh9PSkoKLl68iEePHsHFxQUtWrSAsbHxC+tHRUXh/PnzMDAwQPv27eHo6Pivffzyyy8wMDCAv7+/RnlWVhY2btwIU1NTDB8+vNB1a9euRc2aNeHj41PyGyum9PR0mJubY9GiRZgzZ85/aisyMhIeHh7YtGkTRo4cWUoj/JsQAjdv3sTNmzfx7NkzODg4oHbt2nBzcyv1vv6Lsv4eXubZs2cIDg6WjvX09GBhYYGmTZvC3d29zPt3cHBAnz59sHr16jLvi6iqM9D2AIjov7t16xYuX74sHcfFxeHw4cPo1KkT6tWrJ5W7urqWaTBOTU3FlClTsHPnTjRt2hRubm44d+4cMjMz8e2338LPz0+jfl5eHqZOnYr169ejd+/eePbsGUaOHIlPPvkEM2fOfGlfW7ZswYEDB/D666/DxMREKj916hQmTJgAAOjWrRvs7e2lc9evX0dAQAD+97//lWkwLk1WVlYICAgok6AaGhqKDz74AElJSWjXrh1sbGyQmJiI48ePo169eggMDMSIESNKvd9XUZbfw79RKpWYMGECGjZsiLZt20IIgbt37yIiIgI9e/bE9u3bYW5uXmb9jxgxAk2bNi2z9onoOYKIKp1du3YJAGLdunXl2u/NmzeFo6OjOHjwoFSWnZ0thgwZIgwMDMS1a9c06n/xxRdCJpOJY8eOSWWrV68WAMT+/ftf2tfSpUsFAHH48GGN8nnz5onatWsLU1NT8fPPP2uc+/bbbwUAceDAgVe9xWJJS0sTAMSiRYvKtJ//YsWKFQKAmDVrlnj69KnGucePH4uAgADh5+enpdHplgcPHggAYurUqRrlwcHBAoCYPn26dgZGRKWOa4yJqpDc3FycOHECmzZtQkhICJKSkgrV2bRpE06ePAkAuHz5MoKDgxEeHo7c3Nx/bd/W1hanT59Gjx49pDIDAwPMmjULOTk5+PXXX6XyvLw8fP311+jWrRs6deoklY8bNw4uLi744osvXtpX165dAQBHjx7VKD969Ch69OiBtm3bFnnOyMgIHTp0kMpyc3Nx8uRJ6Tv566+/CvW1efNmaY1nZGQkgoODceHCBen8gwcP8Msvv2DXrl1QqVQvHHNeXh5OnjyJn3/+GQcOHCjy+/+notbWJiUlYfXq1YiLi4MQAhEREdi8eXOx1zTHxsZi+vTp8Pf3x+eff64x4w7k/xxXr16Njz76qNC12dnZ+P3337Fp0yaEhYUhJSVF43xJxhYbG4vVq1fj8ePHGuVZWVlYvXo1rly5Uurfw7+NvySGDx8OCwsLHDhwoMjzly9fxpYtW/DLL78gNjZW49zGjRtx+PDhIq8LDw/Hhg0bpOOXrTF+WR/79u3D7t27NcrOnz+P1atX49atWxrlwcHBOH78uEbZtWvXsGPHDuzatatKru2mKkrLwZyIykBRM8bXr18X7u7uws7OTvj7+4vWrVsLuVwuPvvsM41rLS0txaRJk8Tk... (line truncated to 2000 chars)
3767:       "text/plain": [
3768:        "<Figure size 800x600 with 1 Axes>"
3769:       ]
3770:      },
3771:      "metadata": {},
3772:      "output_type": "display_data"
3773:     },
3774:     {
3775:      "data": {
3776:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAvYAAAIiCAYAAACjTowZAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAfYBJREFUeJzt3XdUVMfbB/AvS1kEKYJ0EEQExQJRY8UuKsHeayxYYmKsPxMxMUZjgqaYGGMSY4/R2BtqxIItiIrGrqCCFEUU266iLLDM+4cvN64UIYIru9/POXsOd+7cuc/cXeDZ2bmzBkIIASIiIiIiKtdk2g6AiIiIiIheHRN7IiIiIiIdwMSeiIiIiEgHMLEnIiIiItIBTOyJiIiIiHQAE3siIiIiIh3AxJ6IiIiISAcwsSciIiIi0gFM7ImItCwnJwdLlizBmTNnXrkthUKBJUuWID4+/tUDo3KlNF9HZWnNmjX4+++/tR0GkU4y4DfPEumfPXv2IDk5+aX17O3t0aVLlzKP58GDBzh9+jRu374Nd3d31KtXD6ampoXWv3btGk6ePAkjIyM0a9YMTk5OLz3HunXrYGRkhJ49e2qUZ2Vl4ffff4eZmRkGDBiQ77hly5bBxcUFHTp0KHnHiunx48ewsLDAF198gU8//fSV2oqNjUXNmjWxatUqDBo0qJQi/JcQAitWrIBarcbgwYMhl8vz1Xn69ClWr16NWrVqoUmTJsVu9/Lly7h8+TKePn0KR0dHeHh4wMvLq7S7oFX379/H5s2b0aZNG3h6epZq28V9HeU9P3kMDAxgaWmJunXrwsfHp1RjKoijoyM6deqEJUuWlPm5iPSNkbYDIKLXLy4uDmfPnpW2k5KSsG/fPrRo0QLVq1eXyqtVq1amif3Dhw/x/vvvY/Pmzahbty68vLwQExODzMxMLFiwAN26ddOon5ubiw8++AArVqxAUFAQnj59ikGDBuHLL7/E5MmTizzXmjVrEBERgXfeeQcVKlSQyqOjozFy5EgAQNu2beHg4CDtu3jxIkJCQvDxxx+XaWJfmqytrRESElJmCfGBAwcwfPhwAIC5uTn69++fr45CocDIkSPxwQcfFCux37ZtGz766COkp6ejadOmsLGxQWpqKo4cOYLq1asjNDQUAwcOLPW+aENycjJGjhyJP//8s9QT++LKe358fX3RpEkTCCFw/fp1HDx4EO3bt8eGDRtgYWFRZucfOHAg6tatW2btE+k1QUR6b8uWLQKAWL58+Ws97+XLl4WTk5PYs2ePVJadnS369u0rjIyMxIULFzTqf/PNN0Imk4lDhw5JZUuWLBEAxF9//VXkuX744QcBQOzbt0+j/LPPPhMeHh7CzMxM/Pnnnxr7FixYIACIiIiI/9rFYnn06JEAIL744osyPU9p6N+/v6hatap4++23RZs2bQqsc+vWLQFAfPDBBy9t7+effxYAxJQpU8STJ0809t29e1eEhISIbt26lUrsb4LTp08LAPlea6WhuK+jwp6f1atXCwBi/PjxpR4bEb0eHLEnokKp1WpER0fj+vXrsLCwQLNmzWBnZ6dRZ9WqVfD09ESzZs1w9uxZXLhwAc7OzmjRogUMDQ2LbN/W1hbHjh1DlSpVpDIjIyNMmTIF69atw6ZNm1CrVi0Az0br582bh7Zt26JFixZS/eHDh+OLL77AN998g44dOxZ6rjZt2gAAIiMj0bZtW6k8MjISgYGBSEhIQGRkJPr166exz8TEBAEBARrX5NixY0hISICFhQWaNm0Ke3t7jXP98ccf8PDwQEBAAGJjY3Hq1CnUqFED9evXBwDcunULhw8fhomJCdq2bQuZrODbnXJzcxEdHY3k5GTY2NigXr16+a7/ixQKBTZs2IDWrVujWrVqAID09HRs27YNgYGBqFKlCg4dOoQbN26gdu3a8Pf3L7K95+VNI5k5cyYcHBwwfPhwxMfHS+cpqcTERIwfPx49e/bE119/... (line truncated to 2000 chars)
3777:       "text/plain": [
3778:        "<Figure size 800x600 with 1 Axes>"
3779:       ]
3780:      },
3781:      "metadata": {},
3782:      "output_type": "display_data"
3783:     }
3784:    ],
3785:    "source": [
3786:     "plot_top_words(amazon_df, 0, \"Top 20 Words in Genuine Reviews\")\n",
3787:     "\n",
3788:     "plot_top_words(amazon_df, 1, \"Top 20 Words in AI Generated Reviews\")"
3789:    ]
3790:   },
3791:   {
3792:    "cell_type": "code",
3793:    "execution_count": 624,
3794:    "id": "93bfa8fb",
3795:    "metadata": {},
3796:    "outputs": [
3797:     {
3798:      "data": {
3799:       "text/html": [
3800:        "<div>\n",
3801:        "<style scoped>\n",
3802:        "    .dataframe tbody tr th:only-of-type {\n",
3803:        "        vertical-align: middle;\n",
3804:        "    }\n",
3805:        "\n",
3806:        "    .dataframe tbody tr th {\n",
3807:        "        vertical-align: top;\n",
3808:        "    }\n",
3809:        "\n",
3810:        "    .dataframe thead th {\n",
3811:        "        text-align: right;\n",
3812:        "    }\n",
3813:        "</style>\n",
3814:        "<table border=\"1\" class=\"dataframe\">\n",
3815:        "  <thead>\n",
3816:        "    <tr style=\"text-align: right;\">\n",
3817:        "      <th></th>\n",
3818:        "      <th>review</th>\n",
3819:        "      <th>label</th>\n",
3820:        "      <th>word_count</th>\n",
3821:        "    </tr>\n",
3822:        "  </thead>\n",
3823:        "  <tbody>\n",
3824:        "    <tr>\n",
3825:        "      <th>25740</th>\n",
3826:        "      <td>i enjoyed this werewolf story the heroine is a wonderful character and her son s are sure to be strong characters in future books the hero is a well rounded character as well and i look forward to...</td>\n",
3827:        "      <td>0</td>\n",
3828:        "      <td>49</td>\n",
3829:        "    </tr>\n",
3830:        "    <tr>\n",
3831:        "      <th>24464</th>\n",
3832:        "      <td>i enjoyed the story i loved the characters i loved the history i enjoyed the way the author portrayed the characters</td>\n",
3833:        "      <td>1</td>\n",
3834:        "      <td>21</td>\n",
3835:        "    </tr>\n",
3836:        "    <tr>\n",
3837:        "      <th>15012</th>\n",
3838:        "      <td>this is a terrfic series that has the characters and plots of a science fiction story it has the appearance of a very dark and disturbing world the characters are not the same as the original movi...</td>\n",
3839:        "      <td>1</td>\n",
3840:        "      <td>155</td>\n",
3841:        "    </tr>\n",
3842:        "    <tr>\n",
3843:        "      <th>31165</th>\n",
3844:        "      <td>rick bragg is one of the most entertaining characters i ve read in a long time this is a very well written book and i am sure you ll enjoy it as much as i do it s a very well written story and i m...</td>\n",
3845:        "      <td>1</td>\n",
3846:        "      <td>68</td>\n",
3847:        "    </tr>\n",
3848:        "    <tr>\n",
3849:        "      <th>27064</th>\n",
3850:        "      <td>very good book and for a beginner the writing is good there is a lot of detail and so on i liked how the characters were developed the story line was interesting and the characters were well devel...</td>\n",
3851:        "      <td>1</td>\n",
3852:        "      <td>89</td>\n",
3853:        "    </tr>\n",
3854:        "    <tr>\n",
3855:        "      <th>15028</th>\n",
3856:        "      <td>this movie is available in both english and french which is a nice bonus i recommend it i really enjoyed the movie the characters and the story were great the acting was great the acting was great...</td>\n",
3857:        "      <td>1</td>\n",
3858:        "      <td>141</td>\n",
3859:        "    </tr>\n",
3860:        "    <tr>\n",
3861:        "      <th>15283</th>\n",
3862:        "      <td>dirty harry is more than a little predictable the two main characters are just too predictable and predictable the movie is also a bit too long and the first half is pretty straight forward the se...</td>\n",
3863:        "      <td>1</td>\n",
3864:        "      <td>201</td>\n",
3865:        "    </tr>\n",
3866:        "    <tr>\n",
3867:        "      <th>26227</th>\n",
3868:        "      <td>no one includes a better mix of action adventure romance and humor in one story than patti larsen and this installment of the blood gold series is no different i love larsen s writing and characte...</td>\n",
3869:        "      <td>0</td>\n",
3870:        "      <td>64</td>\n",
3871:        "    </tr>\n",
3872:        "    <tr>\n",
3873:        "      <th>24942</th>\n",
3874:        "      <td>i have enjoyed this author s work the characters are well developed and the story is well told the story is well written the characters are well</td>\n",
3875:        "      <td>1</td>\n",
3876:        "      <td>27</td>\n",
3877:        "    </tr>\n",
3878:        "    <tr>\n",
3879:        "      <th>25639</th>\n",
3880:        "      <td>wow this was an awesome book the characters were well developed and i enjoyed the story the writing is well done the story is well told and the flow of the story is well developed the author does ...</td>\n",
3881:        "      <td>1</td>\n",
3882:        "      <td>42</td>\n",
3883:        "    </tr>\n",
3884:        "  </tbody>\n",
3885:        "</table>\n",
3886:        "</div>"
3887:       ],
3888:       "text/plain": [
3889:        "                                                                                                                                                                                                        review  \\\n",
3890:        "25740  i enjoyed this werewolf story the heroine is a wonderful character and her son s are sure to be strong characters in future books the hero is a well rounded character as well and i look forward to...   \n",
3891:        "24464                                                                                     i enjoyed the story i loved the characters i loved the history i enjoyed the way the author portrayed the characters   \n",
3892:        "15012  this is a terrfic series that has the characters and plots of a science fiction story it has the appearance of a very dark and disturbing world the characters are not the same as the original movi...   \n",
3893:        "31165  rick bragg is one of the most entertaining characters i ve read in a long time this is a very well written book and i am sure you ll enjoy it as much as i do it s a very well written story and i m...   \n",
3894:        "27064  very good book and for a beginner the writing is good there is a lot of detail and so on i liked how the characters were developed the story line was interesting and the characters were well devel...   \n",
3895:        "15028  this movie is available in both english and french which is a nice bonus i recommend it i really enjoyed the movie the characters and the story were great the acting was great the acting was great...   \n",
3896:        "15283  dirty harry is more than a little predictable the two main characters are just too predictable and predictable the movie is also a bit too long and the first half is pretty straight forward the se...   \n",
3897:        "26227  no one includes a better mix of action adventure romance and humor in one story than patti larsen and this installment of the blood gold series is no different i love larsen s writing and characte...   \n",
3898:        "24942                                                         i have enjoyed this author s work the characters are well developed and the story is well told the story is well written the characters are well   \n",
3899:        "25639  wow this was an awesome book the characters were well developed and i enjoyed the story the writing is well done the story is well told and the flow of the story is well developed the author does ...   \n",
3900:        "\n",
3901:        "       label  word_count  \n",
3902:        "25740      0          49  \n",
3903:        "24464      1          21  \n",
3904:        "15012      1         155  \n",
3905:        "31165      1          68  \n",
3906:        "27064      1          89  \n",
3907:        "15028      1         141  \n",
3908:        "15283      1         201  \n",
3909:        "26227      0          64  \n",
3910:        "24942      1          27  \n",
3911:        "25639      1          42  "
3912:       ]
3913:      },
3914:      "execution_count": 624,
3915:      "metadata": {},
3916:      "output_type": "execute_result"
3917:     }
3918:    ],
3919:    "source": [
3920:     "amazon_df[\n",
3921:     "    amazon_df[\"review\"].str.contains(r\"\\bcharacters\\b\", case=False, na=False)\n",
3922:     "][[\"review\", \"label\", \"word_count\"]].sample(10, random_state=42)"
3923:    ]
3924:   },
3925:   {
3926:    "cell_type": "code",
3927:    "execution_count": 625,
3928:    "id": "355048a8",
3929:    "metadata": {},
3930:    "outputs": [
3931:     {
3932:      "name": "stdout",
3933:      "output_type": "stream",
3934:      "text": [
3935:       "Label Distribution:\n",
3936:       "label\n",
3937:       "0    1130\n",
3938:       "1    2567\n",
3939:       "Name: count, dtype: int64\n",
3940:       "\n",
3941:       "Percentage Distribution:\n",
3942:       "label\n",
3943:       "0    30.57\n",
3944:       "1    69.43\n",
3945:       "Name: count, dtype: float64\n"
3946:      ]
3947:     }
3948:    ],
3949:    "source": [
3950:     "# Reviews containing the word \"characters\"\n",
3951:     "characters_reviews = amazon_df[\n",
3952:     "    amazon_df[\"review\"].str.contains(r\"\\bcharacters\\b\", case=False, na=False)\n",
3953:     "]\n",
3954:     "\n",
3955:     "# Count of Genuine (0) and AI Generated (1)\n",
3956:     "label_counts = characters_reviews[\"label\"].value_counts().sort_index()\n",
3957:     "\n",
3958:     "print(\"Label Distribution:\")\n",
3959:     "print(label_counts)\n",
3960:     "\n",
3961:     "print(\"\\nPercentage Distribution:\")\n",
3962:     "print((label_counts / len(characters_reviews) * 100).round(2))"
3963:    ]
3964:   },
3965:   {
3966:    "cell_type": "code",
3967:    "execution_count": 626,
3968:    "id": "c65b48d6",
3969:    "metadata": {},
3970:    "outputs": [
3971:     {
3972:      "name": "stdout",
3973:      "output_type": "stream",
3974:      "text": [
3975:       "Label Distribution:\n",
3976:       "label\n",
3977:       "0    1373\n",
3978:       "1    3424\n",
3979:       "Name: count, dtype: int64\n",
3980:       "\n",
3981:       "Percentage Distribution:\n",
3982:       "label\n",
3983:       "0    28.62\n",
3984:       "1    71.38\n",
3985:       "Name: count, dtype: float64\n"
3986:      ]
3987:     }
3988:    ],
3989:    "source": [
3990:     "# Reviews containing the word \"recommend\"\n",
3991:     "recommend_reviews = amazon_df[\n",
3992:     "    amazon_df[\"review\"].str.contains(r\"\\brecommend\\b\", case=False, na=False)\n",
3993:     "]\n",
3994:     "\n",
3995:     "# Count of Genuine (0) and AI Generated (1)\n",
3996:     "label_counts = recommend_reviews[\"label\"].value_counts().sort_index()\n",
3997:     "\n",
3998:     "print(\"Label Distribution:\")\n",
3999:     "print(label_counts)\n",
4000:     "\n",
4001:     "print(\"\\nPercentage Distribution:\")\n",
4002:     "print((label_counts / len(recommend_reviews) * 100).round(2))"
4003:    ]
4004:   },
4005:   {
4006:    "cell_type": "markdown",
4007:    "id": "8a8d80d3",
4008:    "metadata": {},
4009:    "source": [
4010:     "These 2 words recommend and characters where very prominently used by AI to write the review on the other hand humans didn't use these words as much."
4011:    ]
4012:   },
4013:   {
4014:    "cell_type": "markdown",
4015:    "id": "b0841ec0",
4016:    "metadata": {},
4017:    "source": [
4018:     "Side Note: - This also tells us one thing without checking the category in which fake reviews are more common than the others. Since, \"characters\" word were used so often by AI its safe to say AI generated reviews are very common in books category."
4019:    ]
4020:   },
4021:   {
4022:    "cell_type": "code",
4023:    "execution_count": 627,
4024:    "id": "bf66d309",
4025:    "metadata": {},
4026:    "outputs": [
4027:     {
4028:      "data": {
4029:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAtUAAAIiCAYAAAAHJDTKAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAfhtJREFUeJzt3XdYFNf7NvB7aYsgXRHQFZVmw4LdWECxICoqWGIwaqxRk/A10QRj1wQ1iSYmGhN7jyX23mussYKKooIYRQWBVaRz3j98mZ8rxcUFFpb7c117xTnzzJxnJogPhzNnZEIIASIiIiIiem962k6AiIiIiKi0Y1FNRERERKQhFtVERERERBpiUU1EREREpCEW1UREREREGmJRTURERESkIRbVREREREQaYlFNRERERKQhFtVERCVYRkYGlixZgitXrmh8rsTERCxZsgR3797VPLFSrCzfh3Xr1uHUqVPaToNIJ8n4RkUietOBAwfw4MGDd8bZ2tqie/fuRZ5PfHw8Ll++jCdPnsDR0REeHh4wNjbOMz4iIgIXL16EgYEBPvjgA9jb27+zjw0bNsDAwAD+/v4q7WlpaVi1ahVMTEzQv3//HMctW7YMlStXRqdOnQp+YWp6+fIlzMzMMGPGDEycOFGjc926dQu1atXC6tWrERgYWEgZ/h8hBG7evImbN28iOTkZdnZ2qFatGpydnQu9L00U9X3IT3JyMtauXStty2QymJubo169enBzcyvy/u3s7NC1a1csWbKkyPsiKmsMtJ0AEZUs4eHhuHr1qrQdFRWFQ4cOoU2bNnBxcZHanZycirSoTkhIwKhRo7BlyxbUq1cPzs7OuHDhAlJSUvDrr7+iR48eKvFZWVkYPXo0VqxYAR8fHyQnJyMwMBDfffcdvvzyy3z7WrduHfbv348uXbqgXLlyUvuZM2cwbNgwAED79u1RqVIlaV9YWBiGDBmCr7/+ukiL6sJkaWmJIUOGFEmRu337dowfPx7Pnj1Dy5YtYW1tjUePHuHkyZNwcXFBcHAwPvroo0Lv930U5X14l8TERAwbNgy1a9dGixYtIITA/fv3cezYMXTs2BGbNm2CmZlZkfX/0UcfoV69ekV2fqIyTRAR5WPr1q0CgFi+fHmx9nvz5k1hb28vDhw4ILWlp6eLvn37CgMDAxEaGqoS/8MPPwg9PT1x/PhxqW3JkiUCgNi7d2++ff38888CgDh06JBK++TJk0W1atWEiYmJWL9+vcq+X3/9VQAQ+/fvf99LVMuLFy8EADFjxowi7UcTCxcuFADEuHHjxKtXr1T2xcbGiiFDhogePXpoKbuS5fHjxwKAGD16tEr72rVrBQDxxRdfaCcxItIY51QT0XvJzMzEqVOnsHr1amzbtg3Pnj3LEbN69WqcPn0aAHD16lWsXbsWR48eRWZm5jvPb2Njg7Nnz6JDhw5Sm4GBAcaNG4eMjAz8/fffUntWVhbmzp2L9u3bo02bNlL7J598AkdHR/zwww/59tWuXTsAwJEjR1Tajxw5gg4dOqBFixa57jMyMkKrVq2ktszMTJw+fVq6J0+fPs3R15o1a6Q5rbdu3cLatWvx77//SvsfP36MDRs2YOvWrVAqlXnmnJWVhdOnT2P9+vXYv39/rvf/bbnNJX727BmWLFmCqKgoCCFw7NgxrFmzRu053JGRkfjiiy/g7++POXPmqIz0A6//Py5ZsgTffvttjmPT09Nx4sQJrF69Gjt27EB8fLzK/oLkFhkZiSVLliA2NlalPS0tDUuWLMG1a9cK/T68K/+C6N+/P8zNzbF///5c91+9ehXr1q3Dhg0bEBkZqbJv1apVOHToUK7HHT16FCtXrpS285tTnV8fe/bswc6dO1XaLl68iCVLliA8PFylfe3atTh58qRKW2hoKDZv3oytW7eWybnsVEZouagnohIut5HqsLAw4ebmJmxtbYW/v79o0qSJkMvlYvbs2SrHWlhYiBEj... (line truncated to 2000 chars)
4030:       "text/plain": [
4031:        "<Figure size 800x600 with 1 Axes>"
4032:       ]
4033:      },
4034:      "metadata": {},
4035:      "output_type": "display_data"
4036:     },
4037:     {
4038:      "data": {
4039:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAAtYAAAIiCAYAAADsE4/JAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAgTlJREFUeJzs3XdUFNfbB/AvdZG2gFIUEEREUVBEImJFxajBhlhji7HFxCTG5KchGo2aBE2i0WiqvWBssffesbeIiIIFFDGiworCAst9//Awb1aKS1xYWL6fc/Yc584zd54ZV3283LljIIQQICIiIiKi12Ko6wSIiIiIiPQBC2siIiIiIi1gYU1EREREpAUsrImIiIiItICFNRERERGRFrCwJiIiIiLSAhbWRERERERawMKaiIiIiEgLWFgTEWlRbm4uFi5ciIsXL752X+np6Vi4cCESEhJePzGqULT5PSpNq1atwrFjx3SdBlG5YcA3LxJVbHv27EFiYuIr4xwcHNCtW7dSz+fJkye4cOECHjx4ADc3N/j7+8PMzKzI+Pj4eJw9exbGxsZo0aIFqlev/spzrFmzBsbGxggPD1drz87OxvLly2Fubo633367wHGLFy+Gs7MzOnbsWPIL01BGRgasrKwwffp0TJo06bX6unbtGry9vbFixQoMHDhQSxn+PyEEli5dCpVKhUGDBkEmkxWIyczMRFRUFBo0aICgoCCN+42NjUVsbCwyMzPh5OQEd3d3eHp6avsSdOrx48fYsGED2rVrBw8PD632ren3KP/3J5+BgQGsra3RsGFD1K1bV6s5FcbJyQldunTBwoULS/1cRBWBsa4TIKLXExcXh0uXLknbd+7cwb59+9C6dWvUqVNHaq9du3apFtZpaWl4//33sWHDBjRs2BCenp44c+YMsrKyMG/ePPTo0UMtPi8vDx988AGWLl2Kzp07IzMzEwMHDsQ333yDTz/9tNhzrVq1Crt378Zbb72FKlWqSO3R0dEYMWIEAKB9+/ZwdHSU9sXExGDYsGGYMGFCqRbW2mRjY4Nhw4aVWkF68OBBvPvuuwAACwsL9O/fv0BMeno6RowYgQ8++ECjwnrz5s0YP348Hj58iObNm8POzg7Jyck4evQo6tSpg4iICAwYMEDr16ILiYmJGDFiBP7880+tF9aayv/9qV+/PoKCgiCEwK1bt3Do0CG8+eabWLduHaysrErt/AMGDEDDhg1LrX+iCkcQkV7ZuHGjACCWLFlSpueNjY0V1atXF3v27JHacnJyRN++fYWxsbG4cuWKWvz3338vDA0NxeHDh6W2hQsXCgBi586dxZ5rzpw5AoDYt2+fWvvkyZOFu7u7MDc3F3/++afavnnz5gkAYvfu3f/1EjXy9OlTAUBMnz69VM+jDf379xe1atUSb7zxhmjXrl2hMffv3xcAxAcffPDK/n755RcBQPzvf/8Tz58/V9uXmpoqhg0bJnr06KGV3MuDCxcuCAAFvmvaoOn3qKjfn6ioKAFAfPzxx1rPjYiKxhFrokpCpVIhOjoat27dgpWVFVq0aAF7e3u1mBUrVsDDwwMtWrTApUuXcOXKFdSoUQOtW7eGkZFRsf1XrVoVJ0+eRM2aNaU2Y2Nj/O9//8OaNWvw119/oUGDBgBejFbPnj0b7du3R+vWraX4d999F9OnT8f333+PTp06FXmudu3aAQAOHDiA9u3bS+0HDhxAhw4dcPPmTRw4cAD9+vVT22dqaoqWLVuq3ZOTJ0/i5s2bsLKyQvPmzeHg4KB2rpUrV8Ld3R0tW7bEtWvXcO7cOdSrVw9NmjQBANy/fx9HjhyBqakp2rdvD0PDwh9dycvLQ3R0NBITE2FnZwd/f/8C9/9l6enpWLduHdq2bYvatWsDAB4+fIjNmzejQ4cOqFmzJg4fPoy7d+/Cx8cHfn5+xfb3b/nTGKZOnQpHR0e8++67SEhIkM5TUrdv38bHH3+M8PBwfPfd... (line truncated to 2000 chars)
4040:       "text/plain": [
4041:        "<Figure size 800x600 with 1 Axes>"
4042:       ]
4043:      },
4044:      "metadata": {},
4045:      "output_type": "display_data"
4046:     }
4047:    ],
4048:    "source": [
4049:     "plot_top_words(yelp_sample, 0, \"Top 20 Words in Genuine Reviews\")\n",
4050:     "\n",
4051:     "plot_top_words(yelp_sample, 1, \"Top 20 Words in AI Generated Reviews\")"
4052:    ]
4053:   },
4054:   {
4055:    "cell_type": "code",
4056:    "execution_count": 628,
4057:    "id": "ac76aa3f",
4058:    "metadata": {},
4059:    "outputs": [
4060:     {
4061:      "data": {
4062:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAA3IAAAIOCAYAAAD9QD/vAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAtDhJREFUeJzs3XdYVEf7N/AvdZGOUqQLKqAidkUjCgo2LFhjN/YYu9Ek2Dtq9JHYu7F3Y4kdBXvHLmABBASlygLC0vb9w5fzc6mLGnHl+7muvZ6cOXNm7jngc+3NzJmjJJVKpSAiIiIiIiKFoVzWARAREREREVHpMJEjIiIiIiJSMEzkiIiIiIiIFAwTOSIiIiIiIgXDRI6IiIiIiEjBMJEjIiIiIiJSMEzkiIiIiIiIFAwTOSIiIiIiIgXDRI6IiL6KVatWQV9fH8nJyWUdSpko7+Mvzw4fPgx9fX08evSorEMp0v3796Gvr48TJ06UdShEJCcmckRECuT8+fPQ19eX63P//v3/NJYdO3bI9GdgYICqVauibdu2OHLkSIH6GRkZSE5OhlQq/U/j+lb91+PP+3nUrl27yD7y6pw/f16uNmNiYjBjxgw0bdoUFhYWsLS0hLOzMwYPHgw/Pz/k5uZ+ySGUqaVLl0JfXx9paWlfvO3MzEwkJycjJyen2Hr5/00ZGhrCwcEBw4cPR1hY2BeP62PZ2dlITk5GVlbWf9oPEX05TOSIiBRIy5YtER4eLvPR0tKCjY1NgfLatWv/p7FIJBIkJydj8+bNCA8PR1hYGE6ePIlq1aqha9euWLlypUz9sWPHIikpCXp6ev9pXN+q/3r869atg7q6Oh4/flxkopb3M5Pny/qJEyfg4OCAgIAA/P7777h27Rpu3bqFhQsXIisrC23atMHff//9hUdRdr6FPzTk/zf15MkTLFu2DKdPn4azszNiY2P/s77r1auHpKQkeHp6/md9ENGXxUSOiEiBqKqqFph5U1JSgoqKSoFyFRWVrxKTlpaW0Ke9vT1WrVoFU1NTbN68WaaeSCQS4i2P/svxBwUF4dq1a/jf//6H6tWrY+PGjZ/V3tOnT9GzZ0+0atUKAQEB8PLygpWVFUxNTdGqVSvs3LkTJ06cgKam5hcaAX0s79+UiYkJPD09sWjRIsTGxmLbtm3/WZ95/x+ipqb2n/VBRF8WEzkiou/Q48eP0bt3b1hbWwtfvo8ePSpTZ8GCBdDX18f79+8xefJk2NjYwNraGiNHjkRCQsIn962kpASRSFQgkSzqGbGrV6+idevWqFy5MurXr4/9+/cX+kxRXrzp6emYOnUq7OzsUK1aNQDA/v37ZZZ4WlhYoH379jhz5kyhY05PT8dvv/0GW1tbVK9eHcuXLwfwYUZkypQpqFq1KqytrTF16tQCywcTEhIwadIk1K5dG6ampmjatCmWLFmCjIyMYu9LYePPi0cikWDmzJmoWrUqLC0tMXTo0FI9S7dx40YYGRmhV69e+Pnnn3HkyBHEx8fLfX1+8+bNQ2ZmJlasWFHkHwTat2+P3r17y5RFR0dj7NixcHBwgLGxMRo2bIg1a9bIzHKVdsylafNTfzfGjRuHBQsWAAAsLCwKXZ4sTxwAcP36dbi7u8v8Pn+umjVrAgDCw8NlyiUSCXx8fNCgQQOYmJjA3t4eU6ZMQUpKilDfwMAAS5YsKdBmYmIijI2NMX36dABFPyNXUh/Z2dmwsLDAjBkzZK6rVasW9PX1ERQUJJTlLQ2/evUqACA3NxfLly9H48aNYWZmhjp16mDMmDGIiYn5jLtFVH4wkSMi+s7cvXsXTZo0QXx8PA4fPoxLly6hQYMG8PLyklnumJ6ejuTkZIwfPx729va4ePEi1q9fj1OnTqF169YlJiaFkUgkWLZsGcLDwzFkyBCZc4UtXbt27RpatWoFAwMDnD17Frt378aFCxdw6NChAs8UfRyvtbU1zpw5g19++QUA0LVrV2FJ... (line truncated to 2000 chars)
4063:       "text/plain": [
4064:        "<Figure size 900x600 with 1 Axes>"
4065:       ]
4066:      },
4067:      "metadata": {},
4068:      "output_type": "display_data"
4069:     }
4070:    ],
4071:    "source": [
4072:     "vectorizer = CountVectorizer(\n",
4073:     "    stop_words=\"english\",\n",
4074:     "    ngram_range=(2,2),\n",
4075:     "    max_features=20\n",
4076:     ")\n",
4077:     "\n",
4078:     "X = vectorizer.fit_transform(amazon_df[amazon_df[\"label\"] == 1][\"review\"])\n",
4079:     "\n",
4080:     "counts = np.asarray(X.sum(axis=0)).flatten()\n",
4081:     "\n",
4082:     "bigrams = vectorizer.get_feature_names_out()\n",
4083:     "\n",
4084:     "pairs = sorted(zip(bigrams, counts), key=lambda x: x[1], reverse=True)\n",
4085:     "\n",
4086:     "bigrams, counts = zip(*pairs)\n",
4087:     "\n",
4088:     "plt.figure(figsize=(9,6))\n",
4089:     "plt.barh(bigrams, counts)\n",
4090:     "plt.title(\"Top Bigrams in AI Generated Reviews\")\n",
4091:     "plt.gca().invert_yaxis()\n",
4092:     "plt.show()"
4093:    ]
4094:   },
4095:   {
4096:    "cell_type": "code",
4097:    "execution_count": 629,
4098:    "id": "f37d5337",
4099:    "metadata": {},
4100:    "outputs": [
4101:     {
4102:      "data": {
4103:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAA1wAAAIOCAYAAACs1AyMAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAp0NJREFUeJzs3XdYVFfbLvB7hjL0IiIoIiAiiij2brBgQUFsiQ1jL7HEGpVEXzUaNRqNicYWC1Gx944FsRc0dmwICCogKDIUGdo+f3jYnyMDDMYRhft3XVzn3Ws/e61nb/A782StvUYiCIIAIiIiIiIi+uikxZ0AERERERFRScWCi4iIiIiISENYcBEREREREWkICy4iIiIiIiINYcFFRERERESkISy4iIiIiIiINIQFFxERERERkYaw4CIiIiIiItIQFlxERJSHp6cnvLy8ijuNYlPa7780Gzx4MGrVqlXcaRTol19+gZmZWXGnQURqYsFFRKQhEyZMgJmZWaE/NWrU0HguvXr1UhrTwsICrq6uGDhwIEJDQ/PEJycnIyUlReN5fa40ff+5v48pU6YUGGNtba12n5cvX8bgwYPh6uoKKysrODk5oVWrVvjpp5/w8OHDj5H2Z6NVq1bo0qWLRvpOTU2FXC4vNO79f1NWVlZo0KAB5s6di/T0dI3kluvNmzdISkrS6BhE9PGw4CIi0pBffvkFkZGR4s/evXuRlJSE0aNHK7VfvHhR47mkpKQgPT1dHPPBgwdYvXo1QkND0aBBA9y/f18p/ujRozh48KDG8/pcafL+Y2JisGvXLujq6mLt2rVQKBQq41JSUvD69Wu1+pw0aRKaNm0KXV1drFq1Cjdv3sSxY8cwdOhQHD16FM7Oznj58uVHvIvi9Tn8B4H3/01dvnwZvXv3xrRp09CrVy+Njj1t2jQkJiZqdAwi+ni0izsBIqKSSl9fH/r6+uKxkZERAEBPT6/YlgO9O27ZsmXx559/onHjxti6dStmzpwpnsvNtbTS5P2vX78e2tra2LFjB1q2bIndu3ejd+/eH9zf77//jkWLFmHt2rUYNGiQ0jkHBwf07NkTfn5+/zVtykfuvykzMzNMmDABFy9exM6dO/Ho0SM4OTlpZEw9PT3o6elppG8i+vg4w0VEVMy2bdsGd3d3WFtbw97eHr6+vnmWgDVt2hS9evXC48eP4ePjgwoVKqBmzZpYsmQJBEH44LFzP7RpaWkptef3DtPSpUtRq1YtlC9fHp06dcK9e/dUvvOSm29ERAS+/vprVKxYEd9//z0AoH///kpLG52cnDBo0CA8efJEZR/h4eHo0qULKlSogCZNmuDcuXMAgLCwMHTt2hU2NjZwc3PD3r178+R79epVdO/eHVWqVEGlSpXQoUMHHDp0qNDnour+c/N5+vQpvv76a1SoUAEuLi74448/Cu0vlyAIWLduHb755hu4u7ujRYsWWLNmjdrXvy89PR2zZ89GgwYN8hRbubS0tLBgwQJYWFgotZ87dw5dunRBpUqVUL58eXh6euL8+fNKMUW956L0+aF/G46Ojrhx4wZOnz6d77JcdfIAgOXLl8PNzU3p7/m/cnFxAQBERkYqtUdGRmLYsGFwcnJCuXLl0LhxY6xfv14pFzMzM9y9ezdPn1u3boWZmZk4G57fO1yFjXHy5EmYmZnh0qVLYtv169dhZmaGunXrKvU1YcIEVK5cWfy/LzExMRg1ahRq1KiBChUqoFmzZvjzzz+RmZlZtAdEVBoJRET0SYSEhAgAhNmzZ4ttc+fOFSQSiTBt2jQhLCxMuHz5stC8eXPBxMREuHPnjhhXo0YN4auvvhI8PDyEoKAgISIiQli8eLGgra0tTJ48udCxO3XqJMhkMqW2mJgYwdvbWzA0NBTu37+vdK5Zs2aCu7u7Utu0adMELS0tYcGCBUJERIRw7tw5oV27doKHh4dgZ2enFJubb9u2bYWTJ08KDx48EPz9/QVB... (line truncated to 2000 chars)
4104:       "text/plain": [
4105:        "<Figure size 900x600 with 1 Axes>"
4106:       ]
4107:      },
4108:      "metadata": {},
4109:      "output_type": "display_data"
4110:     }
4111:    ],
4112:    "source": [
4113:     "vectorizer = CountVectorizer(\n",
4114:     "    stop_words=\"english\",\n",
4115:     "    ngram_range=(2,2),\n",
4116:     "    max_features=20\n",
4117:     ")\n",
4118:     "\n",
4119:     "X = vectorizer.fit_transform(yelp_sample[yelp_sample[\"label\"] == 1][\"review\"])\n",
4120:     "\n",
4121:     "counts = np.asarray(X.sum(axis=0)).flatten()\n",
4122:     "\n",
4123:     "bigrams = vectorizer.get_feature_names_out()\n",
4124:     "\n",
4125:     "pairs = sorted(zip(bigrams, counts), key=lambda x: x[1], reverse=True)\n",
4126:     "\n",
4127:     "bigrams, counts = zip(*pairs)\n",
4128:     "\n",
4129:     "plt.figure(figsize=(9,6))\n",
4130:     "plt.barh(bigrams, counts)\n",
4131:     "plt.title(\"Top Bigrams in AI Generated Reviews\")\n",
4132:     "plt.gca().invert_yaxis()\n",
4133:     "plt.show()"
4134:    ]
4135:   },
4136:   {
4137:    "cell_type": "code",
4138:    "execution_count": 630,
4139:    "id": "a728bb12",
4140:    "metadata": {},
4141:    "outputs": [
4142:     {
4143:      "data": {
4144:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArMAAAJOCAYAAACk64/cAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAi+JJREFUeJzs3XdYFFfbBvB7FxAsNBVEELGgIqixYxdErNiNYI0t9p7E2GsMscYeTew91thrFHvvXUQRFOxSlbZ7vj98mS8rxUUXdhbu33XN9b5z5syZZzYqD8+eOaMQQggQERERERkgpb4DICIiIiL6UkxmiYiIiMhgMZklIiIiIoPFZJaIiIiIDBaTWSIiIiIyWExmiYiIiMhgMZklIiIiIoPFZJaIiIiIDBaTWSIiIiIyWExmiYhSMWrUKBgbGxvMuIaOnwsRfSkms0SUJdRqNTZs2IAmTZrA1tYWpqamKFq0KBo0aIBly5YhNjZW3yHqzLBhw2BmZqbvMFL47bffoFAooFAocP78+VT7VKxYEQqFAs7Ozl90DbneOxFlX0xmiSjTxcXFoXnz5ujTpw88PT1x/vx5REdH49SpU2jatClGjBiBBQsW6DvMLPHbb78hKSlJrzHkzZsXq1atStF+9epVXL9+HXnz5s3ymOTwuRCRYWIyS0SZbujQoTh06BD27t2Ln3/+GcWLF0euXLlQtGhR/PTTT7h8+TKKFCmi7zBzjLZt22LTpk2Ii4vTaF+5ciWcnZ1RsWJF/QRGRPQFmMwSUaZ6+vQpli9fjnbt2qF+/fqp9ilVqhS6dOki7atUKkyfPh0uLi4wNTVFwYIF4evri4cPH2qcZ2VlhX79+uHs2bOoXbs2cufOjUmTJuHUqVNQKBTYs2cP/vjjDzg7O8PIyAiXLl0CANy+fRvffvstbGxsYGpqirJly2L+/PmfvZe5c+dKX9MrFApYWFigfv362L9/v9SndevWmDdvHuLj4zX6BgcHA0h7bujRo0fh6ekJc3Nz5MmTB+7u7ti+fbtGn379+sHKygoxMTHo2bMnrKysYGVlha5duyIqKuqz8Sfr1q0boqKisHPnTqktISEBGzZsQPfu3TPt3pPjj4iIQPfu3ZE/f36ULVs21c/lzZs3KFq0KKpUqaKRdD9//hz29vaoWbMmEhMTtb5nIsq+mMwSUaY6cuQIVCoVmjZtqvU5PXr0wKRJkzBy5Ei8ePECR48eRXBwMNzd3fH48WONvo8fP4a/vz/++usvBAYGonLlytKxFStW4NmzZzh58iQCAgKQO3duXLhwAdWrV0diYiJOnDiB169fY+rUqRg/fjxGjRqVblzDhg2DEAJCCKhUKty8eROVKlVCq1atcOXKFQDAP//8g6FDh8LU1FTqK4RAsWLF0hx39+7d8Pb2hpOTE27duoWgoCDUr18f7dq1w9KlS1P0Hzx4MNq3b4/Q0FD8/fff2LlzJ0aOHKn151ukSBE0bNhQY6rBrl278O7dO3Tr1i3T771fv35o3749goKC0oy7QIEC2LJlC27evInBgwcD+PhLjp+fHxITE7F582aYmJhofc9ElI0JIqJMNGnSJAFAHDlyRKv+V65cEQDEhAkTNNqfPn0qTE1NxXfffSe1WVpairx584o3b95o9D158qQAILy9vVOMX61aNVGqVCkRHx+v0T5r1ixhbGwswsLChBBC/Pzzz8LIyEirmIsVKyYGDRok7Q8dOlSYmpqm2je1cUuXLi1cXFyESqXSaPfy8hJWVlbi/fv3Qggh+vbtKwCIzZs3a/QbPHiwyJUrl0hMTEw3Tn9/fwFA3L17V2zYsEEYGRmJZ8+eCSGEaNasmfR51a5dW5QsWVKLO8/YvSfHv3r16hTH0vq858+fLwCIlStXipEjRwqlUikOHjyoVWxElDOwMktEsvLvv/8C+Div878cHBxQo0YN6XiyOnXqIH/+/KmO1bJlS439Fy9e4OLFi2jVqhVy... (line truncated to 2000 chars)
4145:       "text/plain": [
4146:        "<Figure size 800x600 with 2 Axes>"
4147:       ]
4148:      },
4149:      "metadata": {},
4150:      "output_type": "display_data"
4151:     }
4152:    ],
4153:    "source": [
4154:     "feature_cols = [\n",
4155:     "    \"text_length\",\n",
4156:     "    \"word_count\",\n",
4157:     "    \"sentence_count\",\n",
4158:     "    \"avg_word_len\",\n",
4159:     "    \"vocab_richness\",\n",
4160:     "    \"label\"\n",
4161:     "]\n",
4162:     "\n",
4163:     "corr = amazon_df[feature_cols].corr()\n",
4164:     "\n",
4165:     "plt.figure(figsize=(8,6))\n",
4166:     "plt.imshow(corr)\n",
4167:     "\n",
4168:     "plt.colorbar()\n",
4169:     "\n",
4170:     "plt.xticks(range(len(feature_cols)), feature_cols, rotation=45)\n",
4171:     "\n",
4172:     "plt.yticks(range(len(feature_cols)), feature_cols)\n",
4173:     "\n",
4174:     "plt.title(\"Correlation Matrix\")\n",
4175:     "\n",
4176:     "plt.tight_layout()\n",
4177:     "plt.show()"
4178:    ]
4179:   },
4180:   {
4181:    "cell_type": "code",
4182:    "execution_count": 631,
4183:    "id": "73665682",
4184:    "metadata": {},
4185:    "outputs": [
4186:     {
4187:      "data": {
4188:       "image/png": "iVBORw0KGgoAAAANSUhEUgAAArMAAAJOCAYAAACk64/cAAAAOnRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjExLjEsIGh0dHBzOi8vbWF0cGxvdGxpYi5vcmcvctoD+AAAAAlwSFlzAAAPYQAAD2EBqD+naQAAi95JREFUeJzs3XdYFFfbBvB7KYIiRQFFqiIiYokdFY2gYu8Ne9QYNZZYkhh7T4gxGnuJLXaNLRq7RrHE3k1EBBRFwIJKVdru+f7wZb6sFBdd2Fm4f9c115s5c+bMM/uKPD575oxCCCFARERERKSHDHQdABERERHRh2IyS0RERER6i8ksEREREektJrNEREREpLeYzBIRERGR3mIyS0RERER6i8ksEREREektJrNEREREpLeYzBIRERGR3mIyS0SUhfHjx8PIyEhvxtV3/FyI6EMxmSWifKFSqbBlyxa0bNkSpUqVgomJCZydndGkSROsXr0aSUlJug5Ra0aPHg1TU1Ndh5HJjz/+CIVCAYVCgYsXL2bZp3r16lAoFHBzc/uga8j13omo4GIyS0R5Ljk5GW3atMHgwYPh6+uLixcvIiEhAWfPnkWrVq0wduxYLF68WNdh5osff/wR6enpOo3BzMwMv/32W6b269ev4+bNmzAzM8v3mOTwuRCRfmIyS0R5btSoUTh69CgOHDiA7777DuXKlUORIkXg7OyMb7/9FlevXoWjo6Ouwyw0OnfujG3btiE5OVmtfd26dXBzc0P16tV1ExgR0QdgMktEeerx48dYs2YNunTpgsaNG2fZp0KFCujTp4+0r1QqMWfOHHh4eMDExAQ2Njbw9/dHaGio2nlWVlYYOnQozp8/D29vbxQtWhTTp0/H2bNnoVAosH//fixfvhxubm4wNDTElStXAAD//vsvunXrBltbW5iYmKBSpUpYtGjRe+9lwYIF0tf0CoUCFhYWaNy4MQ4dOiT16dixIxYuXIiUlBS1vuHh4QCynxt64sQJ+Pr6wtzcHMWKFYOXlxd2796t1mfo0KGwsrJCYmIiBg4cCCsrK1hZWaFv376Ij49/b/wZ+vXrh/j4eOzdu1dqS01NxZYtW9C/f/88u/eM+GNjY9G/f3+ULFkSlSpVyvJzefHiBZydnVGrVi21pPvJkyewt7dH/fr1kZaWpvE9E1HBxWSWiPLU8ePHoVQq0apVK43PGTBgAKZPn45x48bh6dOnOHHiBMLDw+Hl5YUHDx6o9X3w4AECAgKwatUqhISEoGbNmtKxtWvXIjIyEmfOnEFgYCCKFi2KS5cuoW7dukhLS8Pp06cRExODWbNmYcqUKRg/fnyOcY0ePRpCCAghoFQqcfv2bdSoUQMdOnTAtWvXAAB//PEHRo0aBRMTE6mvEAJly5bNdtw///wTfn5+cHFxwT///IOwsDA0btwYXbp0wcqVKzP1HzlyJLp27YqIiAhs374de/fuxbhx4zT+fB0dHdGsWTO1qQb79u3Dq1ev0K9fvzy/96FDh6Jr164ICwvLNm5ra2vs2LEDt2/fxsiRIwG8/UdOjx49kJaWht9//x3GxsYa3zMRFWCCiCgPTZ8+XQAQx48f16j/tWvXBAAxdepUtfbHjx8LExMT8dlnn0ltlpaWwszMTLx48UKt75kzZwQA4efnl2n8OnXqiAoVKoiUlBS19p9//lkYGRmJqKgoIYQQ3333nTA0NNQo5rJly4oRI0ZI+6NGjRImJiZZ9s1qXHd3d+Hh4SGUSqVae9OmTYWVlZV4/fq1EEKIIUOGCADi999/V+s3cuRIUaRIEZGWlpZjnAEBAQKACAoKElu2bBGGhoYiMjJSCCFE69atpc/L29tblC9fXoM7z929Z8S/fv36TMey+7wXLVokAIh169aJcePGCQMDA3HkyBGNYiOiwoGVWSKSlb/++gvA23md/+Xg4IB69epJxzM0bNgQJUuWzHKs9u3bq+0/ffoUly9fRocO... (line truncated to 2000 chars)
4189:       "text/plain": [
4190:        "<Figure size 800x600 with 2 Axes>"
4191:       ]
4192:      },
4193:      "metadata": {},
4194:      "output_type": "display_data"
4195:     }
4196:    ],
4197:    "source": [
4198:     "feature_cols = [\n",
4199:     "    \"text_length\",\n",
4200:     "    \"word_count\",\n",
4201:     "    \"sentence_count\",\n",
4202:     "    \"avg_word_len\",\n",
4203:     "    \"vocab_richness\",\n",
4204:     "    \"label\"\n",
4205:     "]\n",
4206:     "\n",
4207:     "corr = yelp_sample[feature_cols].corr()\n",
4208:     "\n",
4209:     "plt.figure(figsize=(8,6))\n",
4210:     "plt.imshow(corr)\n",
4211:     "\n",
4212:     "plt.colorbar()\n",
4213:     "\n",
4214:     "plt.xticks(range(len(feature_cols)), feature_cols, rotation=45)\n",
4215:     "\n",
4216:     "plt.yticks(range(len(feature_cols)), feature_cols)\n",
4217:     "\n",
4218:     "plt.title(\"Correlation Matrix\")\n",
4219:     "\n",
4220:     "plt.tight_layout()\n",
4221:     "plt.show()"
4222:    ]
4223:   },
4224:   {
4225:    "cell_type": "code",
4226:    "execution_count": 632,
4227:    "id": "ad75625e",
4228:    "metadata": {},
4229:    "outputs": [
4230:     {
4231:      "data": {
4232:       "text/html": [
4233:        "<div>\n",
4234:        "<style scoped>\n",
4235:        "    .dataframe tbody tr th:only-of-type {\n",
4236:        "        vertical-align: middle;\n",
4237:        "    }\n",
4238:        "\n",
4239:        "    .dataframe tbody tr th {\n",
4240:        "        vertical-align: top;\n",
4241:        "    }\n",
4242:        "\n",
4243:        "    .dataframe thead tr th {\n",
4244:        "        text-align: left;\n",
4245:        "    }\n",
4246:        "\n",
4247:        "    .dataframe thead tr:last-of-type th {\n",
4248:        "        text-align: right;\n",
4249:        "    }\n",
4250:        "</style>\n",
4251:        "<table border=\"1\" class=\"dataframe\">\n",
4252:        "  <thead>\n",
4253:        "    <tr>\n",
4254:        "      <th></th>\n",
4255:        "      <th colspan=\"8\" halign=\"left\">text_length</th>\n",
4256:        "      <th colspan=\"8\" halign=\"left\">word_count</th>\n",
4257:        "      <th colspan=\"8\" halign=\"left\">sentence_count</th>\n",
4258:        "      <th colspan=\"8\" halign=\"left\">avg_word_len</th>\n",
4259:        "      <th colspan=\"8\" halign=\"left\">vocab_richness</th>\n",
4260:        "    </tr>\n",
4261:        "    <tr>\n",
4262:        "      <th></th>\n",
4263:        "      <th>count</th>\n",
4264:        "      <th>mean</th>\n",
4265:        "      <th>std</th>\n",
4266:        "      <th>min</th>\n",
4267:        "      <th>25%</th>\n",
4268:        "      <th>50%</th>\n",
4269:        "      <th>75%</th>\n",
4270:        "      <th>max</th>\n",
4271:        "      <th>count</th>\n",
4272:        "      <th>mean</th>\n",
4273:        "      <th>std</th>\n",
4274:        "      <th>min</th>\n",
4275:        "      <th>25%</th>\n",
4276:        "      <th>50%</th>\n",
4277:        "      <th>75%</th>\n",
4278:        "      <th>max</th>\n",
4279:        "      <th>count</th>\n",
4280:        "      <th>mean</th>\n",
4281:        "      <th>std</th>\n",
4282:        "      <th>min</th>\n",
4283:        "      <th>25%</th>\n",
4284:        "      <th>50%</th>\n",
4285:        "      <th>75%</th>\n",
4286:        "      <th>max</th>\n",
4287:        "      <th>count</th>\n",
4288:        "      <th>mean</th>\n",
4289:        "      <th>std</th>\n",
4290:        "      <th>min</th>\n",
4291:        "      <th>25%</th>\n",
4292:        "      <th>50%</th>\n",
4293:        "      <th>75%</th>\n",
4294:        "      <th>max</th>\n",
4295:        "      <th>count</th>\n",
4296:        "      <th>mean</th>\n",
4297:        "      <th>std</th>\n",
4298:        "      <th>min</th>\n",
4299:        "      <th>25%</th>\n",
4300:        "      <th>50%</th>\n",
4301:        "      <th>75%</th>\n",
4302:        "      <th>max</th>\n",
4303:        "    </tr>\n",
4304:        "    <tr>\n",
4305:        "      <th>label</th>\n",
4306:        "      <th></th>\n",
4307:        "      <th></th>\n",
4308:        "      <th></th>\n",
4309:        "      <th></th>\n",
4310:        "      <th></th>\n",
4311:        "      <th></th>\n",
4312:        "      <th></th>\n",
4313:        "      <th></th>\n",
4314:        "      <th></th>\n",
4315:        "      <th></th>\n",
4316:        "      <th></th>\n",
4317:        "      <th></th>\n",
4318:        "      <th></th>\n",
4319:        "      <th></th>\n",
4320:        "      <th></th>\n",
4321:        "      <th></th>\n",
4322:        "      <th></th>\n",
4323:        "      <th></th>\n",
4324:        "      <th></th>\n",
4325:        "      <th></th>\n",
4326:        "      <th></th>\n",
4327:        "      <th></th>\n",
4328:        "      <th></th>\n",
4329:        "      <th></th>\n",
4330:        "      <th></th>\n",
4331:        "      <th></th>\n",
4332:        "      <th></th>\n",
4333:        "      <th></th>\n",
4334:        "      <th></th>\n",
4335:        "      <th></th>\n",
4336:        "      <th></th>\n",
4337:        "      <th></th>\n",
4338:        "      <th></th>\n",
4339:        "      <th></th>\n",
4340:        "      <th></th>\n",
4341:        "      <th></th>\n",
4342:        "      <th></th>\n",
4343:        "      <th></th>\n",
4344:        "      <th></th>\n",
4345:        "      <th></th>\n",
4346:        "    </tr>\n",
4347:        "  </thead>\n",
4348:        "  <tbody>\n",
4349:        "    <tr>\n",
4350:        "      <th>0</th>\n",
4351:        "      <td>20215.0</td>\n",
4352:        "      <td>383.558348</td>\n",
4353:        "      <td>402.202223</td>\n",
4354:        "      <td>24.0</td>\n",
4355:        "      <td>117.0</td>\n",
4356:        "      <td>217.0</td>\n",
4357:        "      <td>484.0</td>\n",
4358:        "      <td>2095.0</td>\n",
4359:        "      <td>20215.0</td>\n",
4360:        "      <td>75.199159</td>\n",
4361:        "      <td>77.811015</td>\n",
4362:        "      <td>5.0</td>\n",
4363:        "      <td>23.0</td>\n",
4364:        "      <td>43.0</td>\n",
4365:        "      <td>95.0</td>\n",
4366:        "      <td>381.0</td>\n",
4367:        "      <td>20215.0</td>\n",
4368:        "      <td>1.0</td>\n",
4369:        "      <td>0.0</td>\n",
4370:        "      <td>1.0</td>\n",
4371:        "      <td>1.0</td>\n",
4372:        "      <td>1.0</td>\n",
4373:        "      <td>1.0</td>\n",
4374:        "      <td>1.0</td>\n",
4375:        "      <td>20215.0</td>\n",
4376:        "      <td>4.109831</td>\n",
4377:        "      <td>0.436404</td>\n",
4378:        "      <td>2.545455</td>\n",
4379:        "      <td>3.827659</td>\n",
4380:        "      <td>4.074074</td>\n",
4381:        "      <td>4.352941</td>\n",
4382:        "      <td>7.300000</td>\n",
4383:        "      <td>20215.0</td>\n",
4384:        "      <td>0.803361</td>\n",
4385:        "      <td>0.133560</td>\n",
4386:        "      <td>0.317073</td>\n",
4387:        "      <td>0.704545</td>\n",
4388:        "      <td>0.815789</td>\n",
4389:        "      <td>0.909091</td>\n",
4390:        "      <td>1.0</td>\n",
4391:        "    </tr>\n",
4392:        "    <tr>\n",
4393:        "      <th>1</th>\n",
4394:        "      <td>20192.0</td>\n",
4395:        "      <td>296.262827</td>\n",
4396:        "      <td>298.076633</td>\n",
4397:        "      <td>37.0</td>\n",
4398:        "      <td>93.0</td>\n",
4399:        "      <td>169.0</td>\n",
4400:        "      <td>370.0</td>\n",
4401:        "      <td>1665.0</td>\n",
4402:        "      <td>20192.0</td>\n",
4403:        "      <td>63.140055</td>\n",
4404:        "      <td>63.753927</td>\n",
4405:        "      <td>7.0</td>\n",
4406:        "      <td>19.0</td>\n",
4407:        "      <td>36.0</td>\n",
4408:        "      <td>79.0</td>\n",
4409:        "      <td>322.0</td>\n",
4410:        "      <td>20192.0</td>\n",
4411:        "      <td>1.0</td>\n",
4412:        "      <td>0.0</td>\n",
4413:        "      <td>1.0</td>\n",
4414:        "      <td>1.0</td>\n",
4415:        "      <td>1.0</td>\n",
4416:        "      <td>1.0</td>\n",
4417:        "      <td>1.0</td>\n",
4418:        "      <td>20192.0</td>\n",
4419:        "      <td>3.765257</td>\n",
4420:        "      <td>0.419527</td>\n",
4421:        "      <td>1.666667</td>\n",
4422:        "      <td>3.488372</td>\n",
4423:        "      <td>3.714286</td>\n",
4424:        "      <td>3.977549</td>\n",
4425:        "      <td>7.636364</td>\n",
4426:        "      <td>20192.0</td>\n",
4427:        "      <td>0.721480</td>\n",
4428:        "      <td>0.182635</td>\n",
4429:        "      <td>0.029412</td>\n",
4430:        "      <td>0.593750</td>\n",
4431:        "      <td>0.750000</td>\n",
4432:        "      <td>0.869565</td>\n",
4433:        "      <td>1.0</td>\n",
4434:        "    </tr>\n",
4435:        "  </tbody>\n",
4436:        "</table>\n",
4437:        "</div>"
4438:       ],
4439:       "text/plain": [
4440:        "      text_length                                                             \\\n",
4441:        "            count        mean         std   min    25%    50%    75%     max   \n",
4442:        "label                                                                          \n",
4443:        "0         20215.0  383.558348  402.202223  24.0  117.0  217.0  484.0  2095.0   \n",
4444:        "1         20192.0  296.262827  298.076633  37.0   93.0  169.0  370.0  1665.0   \n",
4445:        "\n",
4446:        "      word_count                                                      \\\n",
4447:        "           count       mean        std  min   25%   50%   75%    max   \n",
4448:        "label                                                                  \n",
4449:        "0        20215.0  75.199159  77.811015  5.0  23.0  43.0  95.0  381.0   \n",

(Output capped at 50 KB. Showing lines 3606-4449. Use offset=4450 to continue.)
</content>
```

---

## Assistant (Plan · MiMo V2.5 Free · 19.3s)

_Thinking:_

Now I have a good picture of the notebook. Let me summarize what markdown cells already exist and what's still missing.

## Current Markdown Cells in the Notebook:

1. **Line 367-372**: `### Label Encoding` - EXISTS
2. **Line 374-380**: `1 = fake/AI-generated, 0 = genuine` - EXISTS (label explanation)
3. **Line 482-488**: `### Column Standardization` - EXISTS
4. **Line 893-898**: `### Duplicate Removal` - EXISTS
5. **Line 977-982**: `### Text Cleaning` - EXISTS
6. **Line 1148-1154**: `### Class Distribution` - EXISTS
7. **Line 1293-1298**: `#### Balance Yelp Dataset` - EXISTS
8. **Line 1300-1306**: `randomly sample 25k from each class to create a balanced subset...` - EXISTS (explanation)
9. **Line 1361-1366**: `### Review Length Filtering` - EXISTS
10. **Line 2170-2176**: `When detecting AI-generated reviews, very short texts provide insufficient linguistic signal to reliably distinguish between human and AI.` - EXISTS (review length filtering rationale)
11. **Line 2256-2262**: `### Exploratory Data Analysis` - EXISTS
12. **Line 2604-2609**: `### Feature Engineering` - EXISTS
13. **Line 2612-2618**: `list the features being created: text_length, word_count, sentence_count, vocab_richness, avg_word_len` - EXISTS (feature list)
14. **Line 2836-2842**: `### Feature Distributions` - EXISTS
15. **Line 4005-4011**: `These 2 words recommend and characters where very prominently used by AI...` - EXISTS (insight note)
16. **Line 4013-4018**: `Side Note: - This also tells us one thing...` - EXISTS (side note)

## What's Missing (from original recommendation list):

Based on the original recommendations, here's what was suggested vs what exists:

**Already Done:**
- Label Encoding section heading ✓
- Label explanation (1=fake, 0=genuine) ✓
- Column Standardization heading ✓
- Duplicate Removal heading ✓
- Text Cleaning heading ✓
- Class Distribution heading ✓
- Balance Yelp Dataset heading + explanation ✓
- Review Length Filtering heading ✓
- Review Length Filtering rationale markdown ✓
- Exploratory Data Analysis heading ✓
- Feature Engineering heading ✓
- Feature list markdown ✓
- Feature Distributions heading ✓- Insight notes about "recommend" and "characters" words ✓
- Side note about books category ✓

**Still Missing (potential additions):**
1. **Title/Intro markdown** at the very beginning - no title cell at the top
2. **Word Clouds section heading** - word clouds are generated but no markdown heading before them
3. **N-grams / Bigrams section heading** - bigram analysis is done but no heading
4. **Correlation Matrix section heading** - correlation plots are generated but no heading
5. **Summary Statistics heading** - summary stats are computed but no heading

Also, there's a minor issue: the `vocab_richness` and `avg_word_length` functions are defined twice (once for Amazon, once for Yelp) - could be mentioned but that's a code issue, not a markdown issue.

Let me present this to the user.

Here's the current state of your notebook's markdown cells:

## Already Added (13 markdown cells)
| # | Location | Content |
|---|----------|---------|
| 1 | Before label encoding | `### Label Encoding` |
| 2 | After label encoding heading | `1 = fake/AI-generated, 0 = genuine` |
| 3 | Before column standardization | `### Column Standardization` |
| 4 | Before duplicate removal | `### Duplicate Removal` |
| 5 | Before text cleaning | `### Text Cleaning` |
| 6 | Before class distribution | `### Class Distribution` |
| 7 | Before balancing Yelp | `#### Balance Yelp Dataset` |
| 8 | After balance heading | `randomly sample 25k from each class...` |
| 9 | Before review length filtering | `### Review Length Filtering` |
| 10 | After filtering analysis | `When detecting AI-generated reviews, very short texts...` |
| 11 | Before EDA | `### Exploratory Data Analysis` |
| 12 | Before feature engineering | `### Feature Engineering` |
| 13 | After feature engineering heading | `list the features being created: text_length, word_count...` |
| 14 | Before distributions | `### Feature Distributions` |
| 15-16 | After n-gram analysis | Insight notes about "recommend" and "characters" words + side note about books category |

## Still Missing (5 suggested additions)
1. **Title cell** at the very top of the notebook (e.g., `# Cross-Domain Fake Review Detection`)
2. **Word Clouds section heading** before the word cloud code cells
3. **N-grams / Bigrams section heading** before the bigram bar charts
4. **Correlation Matrix section heading** before the correlation heatmaps
5. **Summary Statistics heading** before the `.describe()` output

These are all minor - the notebook is already well-documented. Want me to suggest wording for any of these, or are you satisfied with the current state?

---

## User

apart from th headings and stuff what next should i take to move forward with the project should i move forward to feature engineering and start with tokenisation ?

---

## Assistant (Plan · MiMo V2.5 Free · 54.1s)

_Thinking:_

The user is asking about the next steps for their cross-domain fake review detection project. They want to know if they should move forward with feature engineering and tokenization.

Let me think about what they've done so far and what the logical next steps would be:

**Done so far:**
1. Data Loading (Amazon + Yelp datasets)
2. Label Encoding (standardized to 0/1)
3. Column Standardization4. Duplicate Removal
5. Text Cleaning (HTML, URLs, emails, encoding artifacts, etc.)
6. Class Distribution analysis + Balancing (Yelp sampled to 25k per class)
7. Review Length Filtering (removed <20 chars)
8. EDA (distributions, word clouds, n-grams, correlations, summary stats)
9. Basic Feature Engineering (text_length, word_count, sentence_count, vocab_richness, avg_word_len)

**What's next?**

The user is asking about tokenization and further feature engineering. Let me think about what makes sense for a cross-domain fake review detection project.

Key considerations:
1. They're working on **cross-domain** detection - meaning they train on one domain (e.g., Amazon) and test on another (e.g., Yelp), or they need features that transfer well across domains.
2. They've already done basic numerical feature engineering.
3. The next logical steps would be:

**Option A: Traditional ML approach (TF-IDF + handcrafted features)**
- Tokenization (remove stopwords, stem/lemmatize)
- TF-IDF vectorization
- Combine with existing numerical features
- Train classical models (SVM, Random Forest, XGBoost, etc.)

**Option B: Deep Learning approach**
- Tokenization + padding
- Embedding layer (Word2Vec, GloVe, or train from scratch)
- LSTM/GRU or Transformer-based models- More complex, needs more data/compute

**Option C: Pre-trained models (BERT, etc.)**
- Use pre-trained language models
- Fine-tune on the task
- State-of-the-art but heavy

Given that:
1. They have a notebook called "classical model-set-project.ipynb" in the same directory - suggesting they're also working on classical ML models
2. The project is about "Cross-Domain" detection - which is a research challenge
3. They're at the EDA/feature engineering stage

I think the most logical next steps would be:

1. **Text Tokenization & Preprocessing**
   - Remove stopwords
   - Stemming or Lemmatization
   - Tokenize text2. **Text Vectorization**
   - TF-IDF (most common for classical ML)
   - Or CountVectorizer (bag of words)

3. **Combine Features**
   - Merge TF-IDF features with existing numerical features (text_length, word_count, etc.)

4. **Model Training**
   - Start with simple baselines (Logistic Regression, Naive Bayes)
   - Try ensemble methods (Random Forest, XGBoost)
   - Evaluate with proper cross-domain setup

5. **Cross-Domain Evaluation**
   - Train on Amazon, test on Yelp (and vice versa)
   - This is the key challenge of the project

Let me also check what's in the classical model notebook to understand their approach better. But actually, I shouldn't read it in plan mode - I should just provide guidance.

Actually, I can read files - I just can't edit. Let me think about what I know and provide a plan.

The user has already done some basic feature engineering (text_length, word_count, sentence_count, vocab_richness, avg_word_len). They're asking about tokenization next.

My recommendation:
1. Yes, tokenization is the right next step
2. But also think about the overall pipeline:
   - Tokenization → TF-IDF → Model training   - Or Tokenization → Embeddings → Deep learning model

I should ask the user about their preference:
- Do they want to go with classical ML (TF-IDF + traditional models) or deep learning?
- What's their compute setup?
- What's the project requirement (research paper, coursework, etc.)?

Let me provide a thoughtful response.

Good question. You've already done solid EDA and basic feature engineering (text_length, word_count, sentence_count, vocab_richness, avg_word_len). Here's what I'd suggest as next steps:

## Recommended Pipeline

```
Current state: Cleaned text + numerical features
                         ↓
              1. Text Tokenization
                         ↓
              2. Stopword Removal + Stemming/Lemmatization
                         ↓
              3. Text Vectorization (TF-IDF)
                         ↓
              4. Combine with existing numerical features
                         ↓
              5. Model Training + Cross-Domain Evaluation
```

## Key Decision Point

Before I plan further, I need to understand your direction:

**Tool: question**

**Input:**
```json
{
  "questions": [
    {
      "question": "What approach do you want to take for the modeling phase?",
      "header": "Modeling Approach",
      "options": [
        {
          "label": "Classical ML (Recommended)",
          "description": "TF-IDF + Logistic Regression, SVM, Random Forest, XGBoost. Faster to train, easier to interpret, good baseline for cross-domain."
        },
        {
          "label": "Deep Learning",
          "description": "LSTM/GRU with embeddings. More complex, needs more compute, but can capture sequential patterns."
        },
        {
          "label": "Both",
          "description": "Start with classical ML as baseline, then try deep learning for comparison."
        }
      ]
    },
    {
      "question": "What's the primary goal of this project?",
      "header": "Project Goal",
      "options": [
        {
          "label": "Coursework/Academic",
          "description": "Need clear methodology, comparisons, and write-up."
        },
        {
          "label": "Research Paper",
          "description": "Need novel contributions, thorough experiments, and ablation studies."
        },
        {
          "label": "Personal Learning",
          "description": "Focus on understanding the pipeline and getting good results."
        }
      ]
    }
  ]
}
```

**Output:**
```
User has answered your questions: "What approach do you want to take for the modeling phase?"="Both", "What's the primary goal of this project?"="Personal Learning". You can now continue with the user's answers in mind.
```

---

## Assistant (Plan · MiMo V2.5 Free · 14.3s)

_Thinking:_

The user wants:
1. Both classical ML and deep learning approaches
2. Personal learning focus

So the plan should be:
1. Classical ML first (baseline)
2. Then deep learning (for comparison/learning)

Let me provide a clear plan for the next steps.

Good choice. Here's a clear plan for the next phases:

## Phase 1: Classical ML (Baseline) - Do this first

**Step 1: Tokenization & Text Preprocessing**
- Remove stopwords (NLTK has these ready)
- Apply stemming (PorterStemmer - already imported!) or lemmatization
- Tokenize text into word lists

**Step 2: Text Vectorization**
- TF-IDF Vectorizer (sklearn) - captures word importance across documents
- Start with max_features=10,000-20,000 to keep it manageable
- Use unigrams + bigrams (ngram_range=(1,2))

**Step 3: Feature Combination**
- Combine TF-IDF matrix with your existing numerical features (text_length, word_count, sentence_count, vocab_richness, avg_word_len)
- Use `scipy.sparse.hstack` for efficiency

**Step 4: Model Training**
- Start with Logistic Regression (good baseline for text)
- Then try Naive Bayes (MultinomialNB - fast, works well with TF-IDF)
- Then Random Forest / XGBoost

**Step 5: Cross-Domain Evaluation**
- Train on Amazon → Test on Yelp
- Train on Yelp → Test on Amazon
- This is the core challenge of your project

## Phase 2: Deep Learning (After Classical ML works)

- Tokenization with Keras Tokenizer or HuggingFace
- Padding sequences
- Embedding layer (Word2Vec/GloVe or train from scratch)
- LSTM/GRU model
- Compare results with classical ML

---

**My suggestion:** Get Phase 1 working first. The classical ML pipeline will give you:
1. A working baseline to compare against
2. Better understanding of what features matter
3. Experience with cross-domain evaluation

Want me to outline the specific code structure for Phase 1 (tokenization → TF-IDF → model training)?

---

