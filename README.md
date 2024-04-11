# Integrating Jodit Rich Text Editor into a React Application with Next.js

In this tutorial, we'll learn how to integrate the Jodit Rich Text Editor into a React application, specifically using Next.js. Jodit is a powerful WYSIWYG editor that provides a user-friendly interface for creating and editing rich text content.

## Prerequisites

- Basic knowledge of React and Next.js.
- Node.js installed on your machine.
- Familiarity with npm or yarn for package management.

## Getting Started

### Step 1: Setting Up a Next.js Project

If you haven't already set up a Next.js project, you can create one using the following commands:

```bash
npx create-next-app my-jodit-editor-app
cd my-jodit-editor-app
```
## Step 2: Installing Jodit
Next, we need to install the Jodit package along with its React wrapper:

```
npm install jodit-react
# or
yarn add jodit-react
```

## Step 3: Creating the Editor Component
Create a new file named Editor.js inside the components directory of your Next.js project. This component will contain the Jodit editor.

```
/* Imports */
import React, { useState, useRef, useMemo } from 'react';
import dynamic from 'next/dynamic';
import Head from 'next/head';

/* Using dynamic import of Jodit component as it can't render in server side*/
const JoditEditor = dynamic(() => import("jodit-react"), { ssr: false });

/*functions*/
export default function Home() {
  const editor = useRef(null); //declared a null value 
  const [content, setContent] = useState("Worlds best html page"); //declare using state

  /* The most important point*/
  const config = useMemo( //  Using of useMemo while make custom configuration is strictly recomended 
    () => ({              //  if you don't use it the editor will lose focus every time when you make any change to the editor, even an addition of one character
      /* Custom image uploader button configuretion to accept image and convert it to base64 format */
      uploader: {         
        insertImageAsBase64URI: true,
        imagesExtensions: ['jpg', 'png', 'jpeg', 'gif', 'svg', 'webp'] // this line is not much important , use if you only strictly want to allow some specific image format
      },
    }),
    []
  );
  /* function to handle the changes in the editor */
  const handleChange = (value) => {
    setContent(value);
  };

  return (
    <>
    {/* Below is a basic html page and we use Tailwind css to style*/}
    <Head>
      <title>Jodit Rich Text Editor on the Web | Soubhagyajit</title>
      <meta name='author' content='Soubhagyajit Borah'/>
    </Head>
    <main>
      <div className="h-screen w-screen flex items-center flex-col">
        <div className="m-10  flex flex-col items-center">
         <span className="text-2xl text-center">
          
        Jodit Rich Text Editor on the Web
        </span> 
        <div className='text-center'>Author : Soubhagyajit Borah</div>
        <div className='text-center'>visit <a href="https://www.soubhagyajit.com/blogs/how-to-add-jodit-editor-in-a-react-app-next-js" target='_blank' className="text-blue-500">www.soubhagyajit.com</a> for more information</div>
        </div>
        <div className="h-full w-[90vw]">
        {/* This is the main initialization of the Jodit editor */}
          <JoditEditor 
            ref={editor}            //This is important
            value={content}         //This is important
            config={config}         //Only use when you declare some custom configs
            onChange={handleChange} //handle the changes
            className="w-full h-[70%] mt-10 bg-white"
            />
            <style>
              {`.jodit-wysiwyg{height:300px !important}`}
            </style>
        </div>

        <div 
        className="my-10 h-full w-[90vw]"
        >Preview:
        <div dangerouslySetInnerHTML={{ __html: content }}></div>

        </div>
      </div>
    </main>
    </>
  );
}

```
Step 5: Running Your Next.js Application
Finally, you can run your Next.js application using the following command:

```
npm run dev
# or
yarn dev
```

Navigate to http://localhost:3000 in your web browser to see the Jodit Rich Text Editor integrated into your Next.js application.

Resources
GitHub Repository: https://github.com/soubhagyajit/jodit

Try on the web: https://jodit-alpha.vercel.app/

Visit website for code breakdown : https://soubhagyajit.com/blogs/how-to-add-jodit-editor-in-a-react-app-next-js

That's it! You've successfully integrated the Jodit Rich Text Editor into your React (Next.js) application. Feel free to customize the editor's configuration and styling according to your requirements.