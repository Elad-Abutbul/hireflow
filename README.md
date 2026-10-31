# hireflow
AI-powered career platform for smart job matching, resume optimization, personalized job search, application tracking, and career guidance.

## מצב הפרויקט

הושלמה תת־משימה 1.1: שלד pnpm workspace בלבד. אין עדיין אפליקציית לקוח, שרת או קוד TypeScript.

לפני כל משימה יש לקרוא את [PRODUCT](docs/PRODUCT.md), את [ARCHITECTURE](docs/ARCHITECTURE.md) ואת [PROGRESS](docs/PROGRESS.md). עובדים על תת־משימה אחת ועוצרים בסיומה.

## מהו ה־workspace

Monorepo הוא מאגר Git אחד לכמה אפליקציות וחבילות. pnpm workspace מגדיר אילו חבילות שייכות אליו, מנהל את התלויות שלהן ומאפשר קישור מקומי ביניהן. ב־HireFlow נשתמש בו כדי לשמור את הלקוח, השרת וחוזי ה־API באותו מאגר, עם קובץ נעילה משותף.

הדפוסים ב־`pnpm-workspace.yaml` מכינים מקום ל־`apps/*` ול־`packages/*`. כרגע רק חבילת השורש קיימת. התיקיות הבאות מתוכננות, וייווצרו רק בתת־המשימה המתאימה:

| תיקייה עתידית | תפקיד |
| --- | --- |
| `apps/web` | ממשק המשתמש; יתחיל בשלב 1.2 |
| `apps/api` | השרת; יתחיל בשלב 1.3 |
| `packages/contracts` | חוזי API וטיפוסים משותפים; בעת הצורך הראשון |

## כלים ופקודות בדיקה

נדרש Node בטווח `>=24.18.0 <25` ו־pnpm בגרסה `11.9.0`. אלה הגרסאות שנבדקו בעת הקמת השלד; הן אינן טענה לגרסאות העדכניות ביותר. גרסת Node המדויקת לשחזור סביבת הפיתוח היא `24.18.0`, והיא רשומה ב־`.nvmrc`. למשתמשי nvm: אפשר להפעיל `nvm use` מתיקיית הפרויקט לאחר שהגרסה מותקנת.

מתיקיית השורש:

```sh
node --version
pnpm --version
pnpm install --frozen-lockfile
pnpm -r list --depth -1
```

`--frozen-lockfile` בודק שניתן להתקין לפי קובץ הנעילה הקיים בלי לעדכן אותו. כרגע אין תלויות להתקנה; פקודת הרשימה אמורה להציג רק את `hireflow` בשורש.

## תפקיד קובצי הבסיס

| קובץ | תפקיד |
| --- | --- |
| `package.json` | שם חבילת השורש, `private: true` למניעת פרסום שלה לרישום חבילות, גרסת pnpm נבחרת וטווחי הכלים הנתמכים |
| `pnpm-workspace.yaml` | דפוסי תיקיות החבילות ו־`engineStrict: true` לדחיית התקנה בכלים שאינם תואמים לדרישות הגרסה |
| `pnpm-lock.yaml` | תיעוד שנוצר בידי pnpm לצורך התקנות עקביות; יש לשמור אותו ב־Git |
| `.nvmrc` | בחירת גרסת Node למי שמשתמש ב־nvm; הקובץ אינו מתקין או מחליף Node בעצמו |

`package-lock.json` הקודם נבדק: הוא הכיל מפת חבילות ריקה וללא תלויות. הוא הוסר במעבר ל־pnpm, כך שיש מנהל חבילות וקובץ נעילה אחד. אין להפעיל `npm install` לצורך תלויות הפרויקט.

תצורת TypeScript והמהדר יתווספו עם קוד ה־TypeScript הראשון. עדיין אין פקודות `dev`, `build`, `typecheck` או `test`, כי אין קוד להפעיל, לקמפל או לבדוק. בדיקות יישום ו־CI מתוכננות לשלב 1.4; בדיקות שלד ה־workspace שכבר בוצעו מתועדות ב־PROGRESS.

תיעוד רשמי: [pnpm workspaces](https://pnpm.io/workspaces), [הגדרות workspace](https://pnpm.io/settings), [שדות package.json](https://pnpm.io/package_json).
