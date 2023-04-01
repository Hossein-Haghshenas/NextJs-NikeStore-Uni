# وب سایت فروشگاهی nike store

## **مقدمه**

به مستندات پروژه وبسایت فروشگاهی nike store حوش آمدید.
در این مستندات تمام مراحل ساخت پروژه و نحوه اجرای آن و چگونگی دپلوی کردن روی هاست به صورت کامل توضیح داده شده است. شما می توانید از طریق فهرست به تمام بخش های مستندات دسترسی داشته باشید.

## **فهرست مطالب**

- تکنولوژی ها

- آماده سازی ساختار اولیه

- آغاز توسعه پروژه

- پیاده سازی روی هاست

<br>

### تکنولوژی ها

این پروژه با next js ورژن 13.0.5 ساخته می شود.

برای پیاده سازی UI از فریمورک Tailwind css استفاده میکنیم همچنین برای آیکون های پروزه از کتابخانه heroicons استفاده میکنیم.

برای مدیریت state ها از کتابخانه مدیریت استیت redux toolkit استفاده میکنیم.

برای ساخت اسلایدر از کتابخانه splidejs استفاده می کنیم.

برای سهولت در پیاده سازی کلس نیم های شرطی از کتابخانه clsx استفاده می کنیم.

یرای مختصر نوشتن کد های جاوا اسکریپتی از کتابخانه lodash استفاده میکنیم و در نهایت برای نمایش پیام ها به صورت اعلان از کتابحانه react-hot-toast استفاده خواهیم کرد.

### آماده سازی ساختار اولیه

در ابتدا با استفاده از یکی از کامند های زیر نکست جی اس را نصب مینماییم :

```
yarn create next-app nike-store

or

npx create-next-app@latest nike-store
```

بعد از اتمام نصب با یکی از کامند های زیر برنامه را اجرا می کنیم :

```
yarn dev

or

npm run dev
```

سپس به آدرس لوکال هاست مراجعه می کنیم و اگر با صفحه زیر مواجه شدیم یعنی نصب با موفقیت انجام شده است.

![alt text](https://florianherlings.de/public/2020-06-29/homepage.png)

بعد از نصب نکست جی اس استراکچر پروژه را آماده میکنیم.
استراکچر پروژه ما به صورت زیر است :

```
/public
    /images
    /videos
    logo.png
/components
    /app
        cartSlice.js
        store.js
    /cartOptions
        cartCount.js
        cartEmpty.js
        cartItem.js
        index.js
    /utils
        card.js
        clips.js
        newsCard.js
        socialLinks.js
        title.js
    cart.js
    flexContent.js
    footer.js
    header.js
    hero.js
    index.js
    sales.js
    stories.js
/data
    index.js
/pages
    /api
        hello.js
    _app.tsx
    index.tsx
/styles
    globals.css
```

در مرحله بعد کانفیگ های تیلویند را تنظیم میکنیم :

برای این کار ابتدا دو فایل به نام های postcss.config.js و tailwind.config.js در روت میسازیم و به ترتیب کد های زیر را در آنها قرار می دهیم.

// postcss.config.js

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

// tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}", "./data/index.js"],
  theme: {
    extend: {},
    screens: {
      xl: { max: "1200px" },
      lg: { max: "991px" },
      md: { max: "767px" },
      sm: { max: "550px" },
      xsm: { max: "375px" },
    },
  },
  plugins: [],
};
```

برای شخصی سازی بیشتر می توانید به داکیومنت تیلویند مراجعه کنید.

سپس کانفیگ های eslint و next را تنظیم میکنیم.
در این پروژه از کانفیگ های eslint استفاده نشده است.

```js

  images: {
    domains: ["sneakernews.com"],
    formats: ["image/avif", "image/webp"],
  },

  webpack: (config, options) => {
    config.module.rules.push({
      test: /\.mp4/,
      type: "asset/resource",
      generator: {
        filename: "static/[hash][ext]",
      },
    });

    return config;
  },
```

کانفیگ اول برای پشتیبانی برنامه ما از دامنه های فراهم کننده تصاویر پروژه هست و کانفیگ دوم برای پشتیبانی از فرمت mp4 ویدیو های پروژه است

congratulations !!!

حالا ساختار اولیه برنامه ما آماده شده است و می توانیم توسعه برنامه را آغاز کنیم.

<br>

### آغاز توسعه پروژه

در این مرحله از بخش اول وب سایت شروع به ساخت کامپوننت ها می کنیم و کامپوننت هایی که در چندین قسمت استفاده می شوند را به صورت ریوزیبل می سازیم تا کد کمتری نوشته شود و در نهایت برنامه ای بهینه تر داشته باشیم.
