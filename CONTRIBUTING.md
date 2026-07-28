# Contributing

Thanks for improving the FIT Package Validator.

## Local Workflow

1. Create a branch from `main`.
2. Edit `index.html` or the repository docs.
3. Open `index.html` directly in a browser for manual testing.
4. Run the JavaScript syntax check:

```powershell
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const m=html.match(/<script>([\s\S]*)<\/script>/); if(!m) throw new Error('No script block found'); new Function(m[1]); console.log('script syntax ok');"
```

## Pull Requests

- Keep changes focused and easy to review.
- Include screenshots or short notes for UI changes.
- Describe the test data used for date-calculation changes.
- Do not commit customer, booking, supplier, or personal data.

## Date Handling

The app uses local calendar dates by design. Avoid changes that convert user
dates through UTC unless there is a documented reason and regression test data.
