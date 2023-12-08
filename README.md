# Next.js PDF Parser Template 📄🔍

https://github.com/tuffstuff9/nextjs-pdf-parser/assets/57072903/c9e5e5eb-ceeb-4947-b26c-11f87bb26312

## Introduction

I was having some trouble parsing PDFs in Next.js, so I thought I would make this template for anyone else who was facing the same issues as me. I hope this template saves you some time and trouble. It's a basic `create-next-app` with PDF parsing implemented using the [pdf2json](https://github.com/modesty/pdf2json) library and file uploading facilitated by [FilePond](https://github.com/pqina/react-filepond).

## Installation & Setup 🚀

1.  **Clone the repository**:
2.  `git clone [repository-url]`
3.  **Navigate to the project directory**:
4.  `cd nextjs-pdf-parser`
5.  **Install dependencies**:
6.  Windows only: In `app\api\upload\route.ts` on line 22, change `tempFilePath` to a valid path. Make sure it starts from the root drive, for example: `C:/coding/nextjs-pdf-parser/public/${fileName}.pdf`   
7.  ```bash
    npm install
    # or
    yarn install
    ```
8.  **Run the development server**:

    ```bash
    npm run dev
    # or
    yarn dev
    ```

    Visit `http://localhost:3000` to view the application.

## Usage 🖱

Navigate to `http://localhost:3000` and use the FilePond uploader to select and upload a PDF. Once uploaded, the content of the PDF is parsed and printed to the server console (Note: it will not be printed to the browser log).

## Technical Details 🛠

- **nodeUtil is not defined Error**:

  To bypass the `nodeUtil is not defined` error, the following configuration was added to `next.config.js`:

```javascript
const nextConfig = {
  experimental: {
    serverComponentsExternalPackages: ['pdf2json'],
  },
};

module.exports = nextConfig;
```

See more details [here](https://github.com/modesty/pdf2json/issues/303)

- **Blank output from `pdfParser.getRawTextContent()`**:

  This issue might be due to incorrect type definitions. There are two potential solutions:

  1.  **Fix TypeScript definitions**: Update the type definition for PDFParser.

  2.  **Bypass type checking**: Instantiate PDFParser as shown:

      `const pdfParser = new (PDFParser as any)(null, 1);`

  For more details, refer to my comment on [this GitHub issue](https://github.com/modesty/pdf2json/issues/273#issuecomment-1662587255).

## Acknowledgements 🙏

A special thanks to the following libraries and their contributors:

- **[FilePond](https://pqina.nl/filepond/)**: For providing a seamless and user-friendly file uploading experience.
- **[pdf2json](https://www.npmjs.com/package/pdf2json)**: For its efficient and robust PDF parsing capabilities.

## License 📜

MIT License
