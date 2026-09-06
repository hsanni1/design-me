# Design Me — Image Transformation Rules

When the user uploads their own image, treat that image as the **primary subject**. The user's identity and facial appearance must be preserved.

## Never change

When applying a reference design, do not change the person's:

face shape · facial structure · eyes · eyebrows · nose · lips · mouth · teeth · skin tone · skin texture · facial proportions · facial expression · hairline · identity · distinguishing facial features

The person in the uploaded image must remain recognizably the **same person**.

## What Design Me should change

Take the selected visual characteristics from the reference and apply them to the user's image without changing their facial identity.

Reference: a person wearing a bucket hat against a textured green background.
User image: a different person sitting inside a restaurant.

If the user chooses *Person + Hat + Background*, Design Me should:

1. Keep the user's original face.
2. Keep their facial features exactly as they appear.
3. Keep their identity.
4. Preserve their natural expression unless an expression change is requested.
5. Apply the reference's bucket hat style to the user's head.
6. Apply the reference's background style, colour and texture.
7. Match the visual treatment, lighting and composition where appropriate.
8. Integrate the new design elements naturally around the preserved face.

The result should read as **"the user, designed in the style of the reference"** — never **"the reference person with the user swapped in"**.

## Face preservation

Facial preservation has the highest priority.

If the image around the head must be modified, create a precise mask around the face and preserve the original face pixels wherever possible. Do not regenerate the face unnecessarily. Do not use generative editing on the face when the change can be achieved through compositing, masking or colour adjustment. Regenerate a face only when the user explicitly asks for a facial change.

## Reference person vs user person

Never automatically copy the reference person's face onto the user's image. Their face, eyes, nose, mouth and facial identity must not be transferred unless the user explicitly asks for an identity transformation.

- Select **Hat** → transfer only the hat.
- Select **Background** → transfer only the background.
- Select **Typography** → transfer only the typography.
- Select **Style** → transfer the visual treatment, preserving the user's person.

## Handling requests

| User says | Behaviour |
|---|---|
| "Give me the same hat" | Add the reference hat. |
| "Give me the same background" | Apply the reference background. |
| "Make my image look like this" | Apply the design language, preserving identity. |
| "Copy the person" | Ask which parts they want — never replace the face automatically. |
| "Change my face" | An explicit facial editing request, handled separately. |

## Non-destructive editing

Keep the user's original image untouched. Maintain separate editable layers for: original image, person, face, hair, hat, clothing, background, typography, effects, reference elements. The original must always be recoverable.

## Core rule

**Design Me should change the design around the user — not change who the user is.**

Preserve the user's face and identity unless they explicitly request a facial transformation.
