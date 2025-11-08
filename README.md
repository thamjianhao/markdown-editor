# The "Notebook" - Multi-File Markdown Editor

## Project Choice

**The Notebook** is a note-taking application where users can write, manage, and preview multiple Markdown files directly in the browser. Visit the site [here](https://thamjianhao.github.io/markdown-editor/).

## Justification of Tools

I chose to work with **Google Gemini 2.5 Pro** because of its strong reasoning and coding capabilities, as well as its Canvas feature, which allows for a more visual and interactive workflow. 

To maintain a seamless chat history and preserve the continuity of the model's reasoning process, I limited the project to a single-file implementation. As a result, I opted for a **simple HTML file** with embedded **CSS and JavaScript**, rather than a more complex framework like React. This approach kept the project lightweight and easy to iterate on within the Canvas environment. 

Additionally, I integrated two external JavaScript libraries, notably **Marked.js** for Markdown-to-HTML conversion, and **JSZip** for enabling folder downloads in a compressed format. 

## High-Level Approach

My overall strategy was iterative and experiment-driven. I began with a **single comprehensive prompt** that contained all the key details and requirements I could anticipate. This provided a broad foundation and allowed me to assess how well the model understood the overall scope.

From there, I adopted a **refinement-based approach**, using smaller, targeted prompts to develop and improve specific features one at a time. This helped maintain focus and avoid situations where the model might overgeneralise or merge multiple logic components in unintended ways. 

## Final Prompts

### 1. Initial Build Prompt

> Build a browser-based Markdown Editor using plain JavaScript. The application should include three panels: a file list on the left, a Markdown editor in the middle, and a live preview on the right. All data should be saved locally in the browser. Focus on building the core functionality first; styling can be refined later.

**Explanation:**  
This prompt established the foundation of the project, defining the core structure and functionality before moving on to UI refinements.

---

### 2. File Creation Enhancement

> Update the "New File" functionality so that the user can name files directly within the application interface instead of using the default JavaScript `prompt()` popup.

**Explanation:**  
After testing the initial build, I wanted to improve usability by replacing the default browser prompt with a more polished and user-friendly naming interaction.

---

### 3. File Upload Feature

> Add a feature that allows users to upload existing Markdown files into the editor. Display a clear warning if a user attempts to upload a non-Markdown file type.

**Explanation:**  
This enhancement allowed users to import and edit their own Markdown files, improving the tool's practicality while maintaining format validation.

---

### 4. Folder and File Structure

> Expand the file list panel to function like an IDE-style file explorer. Enable users to create folders and organise Markdown files within nested directories.

**Explanation:**  
This iteration introduced folder organisation, allowing for a more scalable and structured workspace similar to professional development environments.

---

### 5. File and Folder Download Feature

> Add functionality for users to download individual files or entire folders as a ZIP archive. 

**Explanation:**  
This prompt implemented export capabilities, allowing users to back up or share their work easily.

---

### 6. Resizable Panels

> Add resizable dividers between the three panels, allowing users to adjust the width of the file list, editor, and preview panes using draggable sliders.

**Explanation:**  
The final feature improved usability and personalisation, enabling users to tailor their workspace layout.

## Instructions

### 1. Clone the Repository

Use the following commands to clone the repository and navigate into the project folder:

```bash
git clone https://github.com/thamjianhao/markdown-editor.git
cd markdown-editor
```

### 2. Open the Application

Since this project is built with plain HTML, CSS, and JavaScript, no additional setup or dependencies are required.

You can launch the application by simply opening the `index.html` file in your web browser. 

### 3. Explore the Features

-   Create Markdown files or folders.
    
-   Upload existing `.md` files (non-Markdown uploads will trigger a warning).
    
-   Edit files in the Markdown editor and preview the formatted output in real time.
    
-   Download individual files or entire folders as ZIP archives.
    
-   Resize panels to customise your layout.

## Challenges & Iterations

### Rename Functionality Breaking After Folder Structure Implementation  

One major challenge occurred when the rename functionality stopped working after introducing the folder structure feature. My initial prompt was:


> The ability to double-click and rename files and folders no longer works after adding the folder structure feature. Please fix.

Despite several iterations, the issue persisted. I decided to investigate the code manually to understand the root cause. After extensive debugging, I discovered that the double-click event was being registered as two single clicks, which prevented the `dblclick` listener from firing correctly.

I then communicated this finding with a more specific prompt:

> I found that double-clicking a file name is currently being registered as two single clicks, which triggers the click event twice and prevents the `dblclick` listener from working. Please adjust the event logic so that double-clicks are properly recognised and used for rename actions.

Providing a more detailed explanation led the model to clearly understand the root cause. Through this process, I learned that **communicating observed behavior with precise context** is important to guide the model toward effective debugging.

---

### Overloading the Model with Too Many Instructions  

Another challenge involved giving the model too many tasks within a single prompt. My initial request combined multiple objectives:

> Enhance the File List panel to mimic an IDE’s file explorer. Include support for uploading Markdown files (with a warning for non-Markdown formats), creating folders to organise files hierarchically, and enabling downloads for both single files and entire folders.

The model’s output was partially functional, but the file structure layout broke where it was stacking the subfiles incorrectly. My follow-up prompt was:

> The folder structure is displaying subfiles horizontally instead of vertically beneath their folders. Please adjust the layout so that files are properly nested in a vertical list under each folder.

However, despite multiple clarifications, the model insisted that the issue was fixed when it wasn’t. At this point, I restarted in a new chat, uploaded the last working version of the code, and focused on a step-by-step, one feature at a time approach (e.g., first upload functionality, then folder creation, then downloads).

This incremental strategy worked much better, producing stable and accurate results. With this, I realised that **singular, focused prompts yield more reliable outcomes** than large, multi-objective instructions, which tend to create entangled logic and regressions.
