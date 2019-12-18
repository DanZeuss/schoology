# schoology

## Prerequisites
Dear reviewer, please, make sure to have `yarn` installed in your environment. To install it, please run:
```
npm install --global yarn
```
You'll also need the following CLI tools: `docker` and `docker-compose` to get it running properly.

## Steps to get the App running
### First step
Download the source code. You could download the source code by accessing it over this link: https://github.com/DanZeuss/schoology/archive/master.zip, or, using the `git` to clone it by running the command:
```
git clone https://github.com/DanZeuss/schoology.git
```
It will download all the source code inside a folder named `schoology`.
### Second step
Before start the building process, please, be sure that there aren't services running in the ports `3000` (Node), `6379` (Redis) and `27017` (MongoDB). Now move to the `schoology` folder by running the command `cd schoology/` and then start the building process running the following command:
```
yarn build
```
The `building` process will move according these steps:
- Installs all dependencies to build and deploy an optimized version of front-end build for production;
- Installs all dependencies to build and deploy the server package for production;
- Download and build all containers for the application. The `app` is using `MongoDB` as database and `Redis` for caching to speed up the API responses;
- Move all config files inside the containers;
- Populate the `MongoDB` with fake data.

If everything wen't well, now you could access the `app` by opening the following url in your browser: `http://localhost:3000`. You will have access to the following page:
![](https://i.ibb.co/qswbJjh/Kapture-2019-12-18-at-3-19-48.gif)


## API methods
All methods are served in the following URL path in the application: `/api/v1/` + `controller` which changes according the business (courses, classes, teachers, etc). The `v1` means the version of the current API, which could be deprecated later.

For this presentation, we have one controller called `courses` and few CRUD methods offered by the URL `/api/v1/courses`.

| URL                   |            Method              | Description                    |Payload                    |
| --------------------- | ------------------------------ | ------------------------------ | --------------------------|
| `/api/v1/courses`     | GET                            | Returns a list of courses      |                           |
| `/api/v1/courses`     | POST                           | Add a new course               |`{ name: String, description: String}`
| `/api/v1/courses/{id}`| DELETE                         | Remove a course by its id      |                           |
| `/api/v1/courses/{id}`| GET                            | Find a course by its id        |                           |
| `/api/v1/courses/search?q=`| GET                       | Search all courses by the name |                           |

Adding a new course:
```
curl -X POST \
  http://localhost:3000/api/v1/courses \
  -H 'Accept: */*' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 389' \
  -H 'Content-Type: application/json' \
  -H 'Host: localhost:3000' \
  -H 'cache-control: no-cache' \
  -d '{
	"name": "Business & Management Studies",
	"description": "A degree in a business-related subject strikes a balance between theoretical and practical work. Many business schools in the UK enjoy good relations with local and global businesses alike, meaning students benefit from cutting edge business techniques as well as high calibre work placements during their time at university."
}'
```


Search by all elements that contains the char `a`:
```
curl -X GET \
  'http://localhost:3000/api/v1/courses/search?q=a' \
  -H 'Accept: */*' \
  -H 'Content-Type: application/json' \
  -H 'Host: localhost:3000' \
  -H 'cache-control: no-cache'

```
