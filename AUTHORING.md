# Content Authoring FAQ

## Student Project Repo Configuration
The app uses the course-level `configurator_class` attribute to determine which, if any, configuration script IN THE CERTIFY APP to use during enrollment.

This *HAS* to match a real class name in the `certify` repo or nothing will happen during the student enrollment process for this course. No repo will be created.

Currently the only `configurator_class` is `RepositoryConfigurator`, so if you'd like to include a repo for your students then include the line `configurator_class: RepositoryConfigurator` after the `description:` tag in the course YAML file.


## Common Problems/Fixes

### IDs must be unique
Any `id:` in the YAML files must be unique to the entire project, otherwise each successive element with `id X` will overwrite the previous `X`.

If you have a lab, question, or lab step showing up out of place, this is probably the issue. Make sure that you're not re-using the same ID.


### Filenames must end in `.yml`
Otherwise the course import will silently fail.

--- 

## Fields that Support Markdown
In general, assume nothing supports Markdown rendering.

We use [redcarpet](https://github.com/vmg/redcarpet) to render markdown.

### Image Slides
```
screens:
	- image-slide:
	  	presenter-script: "Markdown *enabled*"
```

### Video Slides
```
screens:
	- video-slide:
	  	video-script: "Markdown *enabled*"
```

### Lab Slides
```
screens:
	- lab:
		introduction: "Markdown *enabled*"
		steps:
	  		- description: "Markdown *enabled*"
```

### Remote Slides
```
screens:
	- remote-slide:
		url: "Markdown *enabled* for the retrieved content"
		presenter-script: "Markdown *enabled*"
```

### Quiz/Polls/Answers
```
screens:
	- quiz:
		presenter-script: "Markdown *enabled*"
		questions:
			-	title: "Markdown *enabled*"
				options:
					- value: "Markdown *enabled*"
					  response: "Markdown *enabled*"
```

## Supported Markdown Elements

The Lab Introduction and Image Presenter Script are both appropriate for creating large content blocks above a lab or above an image. Both could be used to create a slide with only text.

- [x] Paragraphs, Headers, Blockquotes 
- [x] Phrase Emphasis
- [x] Lists (ordered and unordered)
- [x] Links (Recommend against using these until they default to target=”_blank”)
- [x] Images (I don’t recommend using unless the url persisting is guaranteed)
- [x] Inline Code

Codeblocks are not currently rendered correctly.

To embed videos, use the following code (replacing the youtube video reference code):

```
<div class='container' data-video-url='https://youtu.be/R8OAwrcMlRw'></div>
```


## Webhook payloads we process

## Payloads we process

### Docker CLI
We support some of the commands in the Docker 1.11 CLI

#### login
We support *login*

`verification-type: cli-login`

#### ps
We support *ps*

`verification-type: cli-ps`

### Docker Compose CLI
We support some of the commands in the Docker Compose 1.11 CLI

#### up
We support the *up* command

`verification-type: compose-up`

#### down
We support the *down* command

`verification-type: compose-down`

## Lab Slides

```
  - lab:
      title: TITLE
      id: CLASS-SECTION-lab-01
      introduction: |
        DESCRIPTION OF LAB (markdown enabled)
      steps:
        - description: Step 1 instructions (markdown)
          id: CLASS-SECTION-STEP1
        - description: Step 2 instructions (markdown)
          id: CLASS-SECTION-STEP2
        - description: Step 3 instructions (markdown)
          id: CLASS-SECTION-STEP3
          verifications:
            - verification-type: VERIFY
              id: CLASS-SECTION-STEP3-verification
              success-message: SUCCESS
              failure-message: FAILURE
        - description: Step 4 instructions (markdown)
          id: CLASS-SECTION-STEP4
          verifications:
            - verification-type: pull-request-review-comment
              id: CLASS-SECTION-STEP4-verification
              success-message: SUCCESS
              failure-message: FAILURE
```