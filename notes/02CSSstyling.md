# CSS Styling in next JS

- `@`: This symbol represents the root directory of your Next.js project, it signifies module path alias, which is the configured root directory
- `@`: Often points to the project root directory.
- `@components`: Might map to the components directory.
- `@utils`: Could represent the utils directory.

**Benefits of using aliases**:

- Better file organization: You can group related modules under subdirectories and use aliases to access them conveniently.
- Easier maintenance: As your project grows, changing the alias base path in one place affects all imports, reducing potential errors.
- Cleaner code: Aliases shorten long relative paths, making your code more readable.

## Global Styles

- You can import global.css in any component in your application, but it's usually good practice to add it to your top-level component. In Next.js, this is the root layout (more on this later).

In `app/layout.tsx` add -

```tsx
import '@/app/ui/global.css';
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## CSS Module

- CSS Modules create unique class names for each component, so you don't have to worry about style collisions.
- CSS Modules allow you to scope CSS to a component by automatically creating unique class name
  Create `home.module.css` in `app/ui` -

```css
.shape {
  height: 0;
  width: 0;
  border-bottom: 30px solid black;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```

use it in component like this -

```tsx
import styles from '@/app/ui/home.module.css';
<div className={styles.shape} />;
```

## Tailwind css

- a better option than css

## `clsx` library

- its a library that lets you toggle class names easily
- Suppose that you want to create an InvoiceStatus component which accepts status.
- The status can be 'pending' or 'paid'.If it's 'paid', you want the color to be green🟩. If it's 'pending', you want the color to be red🔴.

app/ui/invoices/status.tsx -
```tsx
import clsx from 'clsx';
 
export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-red-500 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```
