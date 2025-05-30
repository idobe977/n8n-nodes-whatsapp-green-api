![Banner image](https://user-images.githubusercontent.com/10284570/173569848-c624317f-42b1-45a6-ab09-f0ea3c247648.png)

# n8n-nodes-green-api

ספריית נודים עבור Green API ל-n8n עם תמיכה בטריגרים מפולטרים

## התקנה

### בהתקנה מקומית

1. הריץ את הפקודה הבאה בתיקיית ההתקנה של n8n שלך (בדרך כלל: `~/.n8n/custom`):
   ```
   npm install n8n-nodes-green-api
   ```

2. התחל מחדש את n8n

### בהתקנה באמצעות Docker

הוסף את המשתנה הסביבתי הבא לקונטיינר שלך:
```
NODE_EXTRA_PACKAGES=n8n-nodes-green-api
```

## שימוש

הנוד מאפשר אינטגרציה עם Green API לשליחת הודעות WhatsApp וניהולן, וכן הקשבה לwebhooks נכנסים.

הוא מספק את המשאבים הבאים:
- **הודעות**: שליחה, עריכה ומחיקה של הודעות 
- **קבוצות**: יצירה וניהול של קבוצות WhatsApp
- **צ'אטים**: קבלת היסטוריית צ'אט
- **אנשי קשר**: קבלת רשימת אנשי קשר
- **טריגר**: הקשבה לwebhooks נכנסים עם פילטרים מתקדמים

## פונקציית הטריגר החדשה

הנוד כולל כעת יכולת טריגר מתקדמת שמאפשרת לך לסנן webhooks נכנסים לפי קריטריונים שונים:

### אפשרויות פילטור

1. **פילטר סוג צ'אט**:
   - כל הצ'אטים
   - צ'אטים פרטיים בלבד (מסתיימים ב-@c.us)
   - קבוצות בלבד (מסתיימות ב-@g.us)

2. **פילטר סוג הודעה**:
   - כל ההודעות
   - הודעות נכנסות בלבד
   - הודעות יוצאות בלבד
   - הודעות טקסט בלבד
   - תמונות בלבד
   - סרטונים בלבד
   - קבצי שמע בלבד
   - מסמכים בלבד
   - מיקומים בלבד
   - אנשי קשר בלבד
   - סקרים בלבד

3. **פילטר צ'אט ספציפי**:
   - מאפשר להגביל את הטריגר לצ'אט ספציפי בלבד

4. **פילטר מילות מפתח**:
   - מאפשר להגביל את הטריגר להודעות שמכילות מילות מפתח מסוימות

### דוגמה לשימוש

1. בחר "Trigger" כמשאב
2. בחר "Webhook" כפעולה
3. הגדר את הפילטרים הרצויים
4. העתק את כתובת הwebhook
5. הגדר את הwebhook בGreen API Dashboard שלך

**דוגמת תרחיש**: טריגר רק כאשר מקבלים הודעת טקסט בקבוצה המכילה את המילה "עזרה":
- Chat Type Filter: Group Chats Only
- Message Type Filter: Text Messages Only  
- Keyword Filter: עזרה

## בעיות ידועות

### בעיית התאמתות של אישורי התחברות

כאשר מכניסים את פרטי ההתחברות (ID והטוקן), אתה עשוי לראות הודעת שגיאה אדומה המציינת שההתחברות נכשלה, אפילו כאשר הפרטים נכונים. זוהי בעיה ויזואלית בממשק המשתמש של n8n.

**פתרון**: התעלם מההודעה האדומה והמשך לעבוד עם הנוד. הקרדנשיאלס באמת נשמרים ויפעלו כראוי בזמן ריצה.

### שימוש בנוד כ-Tool עבור AI Agent

כדי להפוך את הנוד שלך לזמין כמכשיר עבור סוכן ה-AI של n8n, תצטרך לעדכן את קובץ ה-node.ts שלך כדי להוסיף את תכונת `usableAsTool: true`.

אם המאפיין גורם לשגיאות לינטר בזמן הקומפילציה, ייתכן שתצטרך לעדכן את הטיפוסים שלך או לבדוק את התאמת הגרסה עם n8n.

לפרטים נוספים אודות API של Green API, ראה את [התיעוד הרשמי](https://green-api.com/en/docs/).

## פיתוח

אם תרצה לפתח ולהרחיב את הנוד:

1. שכפל את המאגר
   ```
   git clone https://github.com/idobe977/n8n-nodes-whatsapp-api-green.git
   ```
2. התקן תלויות
   ```
   cd n8n-nodes-whatsapp-api-green
   pnpm install
   ```
3. בנה את הנוד
   ```
   pnpm build
   ```
4. קשר את הנוד לתיקיית n8n המקומית שלך לבדיקות
   ```
   pnpm link
   ```

## רישיון

[MIT](LICENSE.md)
