# הגדרת הרשאות חיבור Gmail וDrive ל Make

כדי לבצע אינטגרציה לישומי Google יש להגדיר OAuth בממשק של Google Cloud Console. 
היישומים של google הנפוצים ביותר הם Gmail וDrive (בDrive כלולים גם docs, sheets, forms, slides ועוד)
ולכן במדריך זה נתיחס רק להגדרת 2 ישומים ראשיים אלו.
שלבי הגדרת OAuth בGoogle
* ליצור פרויקט ב Google Cloud Console
* לאפשר API's
* להגדיר מסך ההסכמה לאימות
* להגדיר את אישורי המשתמש שלך
* לחבר בMake עם האישור המותאם
## שלב 1: יצירת פרויקט ב Google Cloud Console
התחברו ל https://console.cloud.google.com/ עם חשבון המשתמש אותו תרצו להגדיר.
בתפריט העליון לחצו על  Select a project ובחרו בNew project
הזינו שם לפרויקט (אפשר להשתמש בשם Make לדוגמא)
לחצו על Create

במסך הראשי לחצו שוב בתפריט Select a project ובחרו בפרויקט החדש שנוצר
יש לוודא ששם הפרויקט מופיע בתיבה

## שלב 2 : הגדרת API's הכלולים בהרשאה זו
בתפריט השמאלי בחרו ב APIs & Services ואז בתפריט השמאלי ב  Library


הקלידו בשורת החיפוש gmail api ובחרו בתוצאת החיפוש בGmail API
לחצו על Enable

יש לחזור על שלבים 1-3 עבור Google Drive API




## שלב 3: הגדרת מסך אימות OAuth
בשלב זה מגדירים את הפרטים הטכניים שיוצגו במסך האימות של google שיוצג בהתחברות.
בתפריט השמאלי לחצו על OAuth consent screen.
תחת User Type, בחרו בExternal
לחצו Create
.


מלאו את שדות החובה במסך זה
בApp Name הכניסו שם מייצג כל שהוא לדוגמא Make
בUser Support Email הכניסו את כתובת המייל של חשבון זה.
בAuthorized domains לחצו על Add Domain והכניסו שם 2 כתובות דומיין:
make.com
integromat.com
בDeveloper contact information הכניסו שוב את כתובת המייל של חשבון זה.
לחצו על Save And Continue



במסך הבא יש הגדרת Scopes תחומי ההרשאה. לחצו על Add or remove scopes
בחלונית הימנית שנפתחה יש לבחור את הScopes הנדרשים לפי הטבלה המצורפת, יש לכתוב בשורת הFilter את המילה gmail כדי לקבל את כל הscopes של gmail ואת המילה drive בשביל scopes של drive.
#### Gmail Api
```
https://mail.google.com/
https://www.googleapis.com/auth/gmail.labels
https://www.googleapis.com/auth/gmail.send
https://www.googleapis.com/auth/gmail.readonly
https://www.googleapis.com/auth/gmail.compose
https://www.googleapis.com/auth/gmail.insert
https://www.googleapis.com/auth/gmail.modify
https://www.googleapis.com/auth/gmail.metadata
```
#### Drive Api
```
https://www.googleapis.com/auth/drive
https://www.googleapis.com/auth/drive.readonly
```
לאחר סימון כל הרשימה הנדרשת
יש ללחוץ על Update
ולאחר מכן לחצו על Save and continue בתחתית העמוד של Scopes

בשלב הבא Test Users אין צורך למלא כלום, יש ללחוץ על Save And Continue
בעמוד האחרון בשלב זה יש סיכום של כל המידע שהוזן עד כה, יש לגלול למטה וללחוץ על Back To Dashbord
בעמוד הבא יש ללחוץ על Publish App



## שלב 4: הגדרת אישורי המשתמש
בתפריט השמאלי לחצו על Credentials.
בתפריט העליון בחרו בCreate Credentials וברשימה בחרו ב OAuth client ID.
בשדה  Application type בחרו ב Web application.
בשדה Name הכניסו שם מייצג לדוגמא Make.
ב Authorized redirect URIs לחצו על + Add URI. והכניסו את הכתובת הבאה:
https://www.integromat.com/oauth/cb/google-restricted 
לחצו על Create

העתיקו את הערכים של Client ID ושל Client secret ושמרו אותם במקום בטוח. נתונים אלו ישמשו אתכם להתחברות בMake.
התחברות לאפליקצית Gmail / Drive מMake
בסנריו בMake הוסיפו מודול של Gmail או Drive
בשדה Connection לחצו על Add
בחלונית שנפתחה יש להזין שם משמעותי לחיבור זה (מומלץ להשתמש בשם המייל)
סמנו בתחתית החלונית Show advanced settings ויופיעו 2 שדות להכנסת הClient ID והClient Secret ששמרתם בשלב קודם
הכניסו את הערכים ולחצו על Sign In with Google.
תפתח חלונית הזדהות של Google
יש לבחור בחשבון של המייל המיועד לחיבור ולהזין סיסמא
תופיע חלונית אזהרה שהאפליקציה לא אומתה ע"י גוגל
יש ללחוץ על מתקדם ועל כניסה אל integromat.com (לא מאובטח)
בחלונית הבאה יש לסמן V בכל ההרשאות, שימו לב! ההרשאה ניתנת לשימושכם בלבד דרך Make ואינה מאפשרת לגורמים אחרים לגשת לחשבון, לכן אין לחשוש לסמן הגדרה זו.
לחצו על המשך
וסיימנו!



במידה ונתקלים בבעיה כל שהיא בשלב זה יש לחזור חזרה על כל השלבים ולוודא שבוצעו כראוי
שגיאות נפוצות:
לא הוגדר Publish App בשלב 3 סעיף 13
לא הוגדרו כראוי כל הscopes הנדרשים בשלב 3

