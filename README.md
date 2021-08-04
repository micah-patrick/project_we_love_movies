![We Love Movies](https://raw.githubusercontent.com/micah-patrick/project_we_love_movies-server/main/readme/readme-header.png "We Love Movies")

#
# We Love Movies

Thinkful backend capstone. This is an API for an app that displays movies, what theaters they are showing at, and reviews of the movies. This API is built using node.js, express, and knex query builder.

#
## SKILLS USED
* Node.js 
* Express
* Knex 
* Cors
* Dotenv

#
## TABLES
![ERD](https://raw.githubusercontent.com/micah-patrick/project_we_love_movies-server/main/readme/erd.png "ERD")
#
### Critics

The `critics` table represents movie critics who have created reviews for movies. Each critic has the following fields:

- `critic_id`: (Primary Key) A unique ID for the critic.
- `preferred_name`: (String) The critic's preferred first name.
- `surname`: (String) The critic's last name.
- `organization_name`: (String) The name of the organization the critic works for.

An example record looks like the following:

```json
{
  "critic_id": 1,
  "preferred_name": "Chana",
  "surname": "Gibson",
  "organization_name": "Film Frenzy"
}
```
#
### Movies-Theaters

The `movies_theaters` table is a join table that connects movies with theaters. It represents which movies are being shown in which theaters. It also includes a key that represents whether or not a movie is currently showing at the theater, or if it has in the past.

- `movie_id`: (Foreign Key) A reference ID to a particular movie.
- `theater_id`: (Foreign Key) A reference ID to a particular theater.
- `is_showing`: (Boolean) A representation of whether or not the movie is currently showing in the referenced theater.

An example record looks like the following:

```json
{
  "movie_id": 1,
  "theater_id": 3,
  "is_showing": false
}
```
#
### Movies

The `movies` table represents movies stored in the application database. Each movie has the following fields:

- `movie_id`: (Primary Key) A unique ID for the movie.
- `title`: (String) The title of the movie.
- `runtime_in_minutes`: (Integer) The length of the movie in minutes.
- `rating`: (String) The rating given to the movie.
- `description`: (String) A shortened description of the movie.
- `image_url`: (String) A URL to the movie's poster.

An example record looks like the following:

```json
{
  "movie_id": 1,
  "title": "Spirited Away",
  "runtime_in_minutes": 125,
  "rating": "PG",
  "description": "Chihiro and her parents are moving to a small Japanese town in the countryside, much to Chihiro's dismay. On the way to their new home, Chihiro's father makes a wrong turn and drives down a lonely one-lane road which dead-ends in front of a tunnel. Her parents decide to stop the car and explore the area. They go through the tunnel and find an abandoned amusement park on the other side, with its own little town...",
  "image_url": "https://imdb-api.com/images/original/MV5BMjlmZmI5MDctNDE2YS00YWE0LWE5ZWItZDBhYWQ0NTcxNWRhXkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_Ratio0.6791_AL_.jpg"
}
```
#
### Reviews

The `reviews` table represents a review done by a critic of a single movie. It references both a critic and a movie.

- `review_id`: (Primary Key) A unique ID for the review.
- `content`: (Text) The content of the review, written in markdown.
- `score`: (Integer) A numerical representation of the score given to the movie by the critic.
- `critic_id`: (Foreign Key) A reference ID to a particular critic.
- `movie_id`: (Foreign Key) A reference ID to a particular movie.

An example record looks like the following:

```json
{
  "review_id": 1,
  "content": "...",
  "score": 4,
  "movie_id": 1,
  "critic_id": 4
}
```
#
### Theaters

The `theaters` table represents movie theaters. Each theater has the following fields:

- `theater_id`: (Primary Key) A unique ID for the theater.
- `name`: (String) The name of the theater.
- `address_line_1`: (String) The first line of the address of the theater.
- `address_line_2`: (String) The second line of the address of the theater.
- `city`: (String) The city in which the theater is located.
- `state`: (String) The state in which the theater is located.
- `zip`: (String) The zip in which the theater is located.

An example record looks like the following:

```json
{
  "theater_id": 1,
  "name": "Hollywood Theatre",
  "address_line_1": "4122 NE Sandy Blvd.",
  "address_line_2": "",
  "city": "Portland",
  "state": "OR",
  "zip": "97212"
}
```

#
## ROUTES

#
### Get all movies

This route will return a list of all movies. Different query parameters will allow for limiting the data that is returned.

There are two different cases to consider:

- `GET /movies`
- `GET /movies?is_showing=true`

#
### Read one movie

These routes will return a single movie by ID.

- `GET /movies/:movieId`
- `GET /movies/:movieId/theaters`
- `GET /movies/:movieId/reviews`

This route should return all the `theaters` where the movie is playing.
```
GET /movies/:movieId/theaters
```


This route should return all the `reviews` for the movie, including all the `critic` details added to a `critic` key of the review.
```
GET /movies/:movieId/reviews
```

#
### Destroy review

This route will delete a review by ID. If the ID is incorrect, a `404` will be returned.

```
DELETE /reviews/:reviewId
```

The server will respond with `204 No Content`.

#
### Update review

This route will allow you to partially or fully update a review. If the ID is incorrect, a `404` will be returned.

```
PUT /reviews/:reviewId
```

#
### Get all theaters

This route will return a list of all theaters. Different query parameters will allow for additional information to be included in the data that is returned.

- `GET /theaters`