# Promise All

Na hoeveel tijd zal deze code "done!" op het scherm tonen? Voer de code dus niet uit maar denk even zelf na.

```typescript
function delay(delay: number): Promise<void> {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve();
        }, delay);
    });
}

async function runMe() {
    await Promise.all([delay(1000), delay(10000), delay(15000)])
    console.log("Done!");
};

runMe();
```
