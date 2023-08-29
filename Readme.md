# Mock server for the interview

## Installation

Clone the repo and run `npm install`. Then do `npm run dev` to start the mock server. It will be running at `apiPort`, which is set to `5678`. Change if needed in `index.js`.

### CORS

Cors is set to allow calls from `appPort`, default is `5173`, change if needed in `index.js`.

## Available endpoints

- `GET /assets`

  List available asset uids.
  Response:

  ```
  {
    data: Array<string>
    error: null | {message: string, code: number}
  }
  ```

- `GET /assets/:asset_uid`

  Given `asset_uid` details.
  Response:

  ```
  {
    data: {
      id: string
      mime_type: string     // e.g. "video/mp4"
      feed_id: string
      creation_date: string // date in UTC, e.g. "2023-07-13T18:28:39.231212"
      title: string
      thumbnail: string     // full URL
      media_url: string     // full URL
      height: number        // in pixels
      width: number         // in pixels
      duration: number      // in seconds
      fps: number           // frames per second, 0 for images
      processing_info: {
        status: string      // "success" or "error"
        start: string       // date in UTC
        end: string         // date in UTC
      }
    }
    error: null | {message: string, code: number}
  }
  ```

- `GET /assets/:asset_uid/persons`

  List the Persons detected in the given `asset_uid`.Response:

  ```
  {
    data: [
      {
        id: string            // e.g. "1347ab6e-d3ea-486f-8750-d819397e148b"
        name: string          // e.g. "Lindsay Lohan"
        appearances: [
          {
            start: number     // detection start time in seconds
            end: number       // detection end time in seconds
            thumbnail: string // full URL
            face_ids: Array<string>
          }
        ]
      }
    ]
    error: null | {message: string, code: number}
  }
  ```

## Take home project:

Vidrovr's Dashboard is our main user-facing product that allows users to upload videos, create input feeds, and view Vidrovr's processing results on those videos.

For this interview, we would like you to re-create a subset of our Dashboard features using our various APIs. We would like you to display the `title` and `creation_date` of a video and the video itself.


### Details

For the purpose of this project, we use the terms “video” and “asset” interchangeably.

Given this mock API, we would like you to create the Metadata Inspector Page of our Dashboard. The metadata page allows users to view all the extracted insights for a video, in this case, we have provided the endpoint for recognized people, which you'll only use if you go for the bonus points.

You can find information on how to install and run locally this API above. You should leverage this mock API to display an asset, its title, creation date and a playable video.

#### Metadata Inspector Page

The inspector page at `/media/<asset_uid>` contains the results of Vidrovr’s processing on a video, as well as the video itself.

The following metadata should be rendered on this page:

- Video Asset - the main video or image component
- Asset title
- Asset creation date

Since the metadata inspection page is associated with specific assets retrieved via uuid at `/media/<asset_uid>`, users should be able to enter an `asset_uid` parameter on the browser URL and have the metadata associated with that video rendered.

The metadata related to the video can be obtained via the `assets/asset_uid` API endpoint.

### BONUS POINTS
- Display another page (`/media`) with a list of the available assets, clicking on an element of this list routes the user to the inspector page (`/media/<asset_uid>`)
- Display a list in the inspector of the detected persons and how many times each person was detected. For person detections use GET `/assets/:asset_uid/persons`

### Deliverables

Please send via email the following:

- Zipped file containing all the code except build files and package files such as node_modules, or the public link to your project in github. Feel free to submit it as a pull request for this repo too, whatever is easier for you.
- File(s) containing any wireframes, hand drawings or sketches showing your design decisions. Alternatively, send a shareable link to a web-based design software such a Figma, Sketch, Google Drawings, Adobe XD etc.

### Constraints, and Targets

- Feel free to use whatever packages and javascript-based frameworks you are comfortable with, but please be sure to write a README detailing how to install and run your code.
- Feel free to use any javascript packages and component libraries
- Readability counts. We look for thoughtfulness in code organization and documentation
- Runnability counts. We'd love to see code that runs without raising errors
- Design & Creativity counts. We’d like for you to exercise your creative chops. We’d also like to see you document your trade-off and design considerations.
