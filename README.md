# Cursos USACH

web platform to find reviews and rate courses of the University of Santiago, Chile.

## technologies

- [Next 13](https://nextjs.org/docs) using the App router
- TypeScript
- [Zod](https://zod.dev/)
- Tailwind CSS
- [LibSQL Client](https://docs.turso.tech/reference/client-access/javascript-typescript-sdk)
- [HeroIcons](heroicons.com/)

## getting started

we recommend the use of [pnpm](https://pnpm.io/), but feel free to use other package managers like npm or yarn

create a `.env.local` file in the root folder, you can get the auth token by using `turso db tokens create NAME_OF_YOUR_DB`, if you need the name of your db and the url you can use `turso db list` 

the `.env.local` file should look like this

```zsh
DB_URL=HERE_GOES_THE_TURSODB_URL
DB_AUTHTOKEN=HERE_GOES_YOUR_TURSODB_TOKEN
```

install dependecies

```zsh
pnpm install
```

run the development server

```zsh
pnpm run dev
```

## database

we are using [Turso DB](https://turso.tech/pricing) for it's generous free tier, it uses LibSQL a fork of SQLite

these are the initial tables, you can connect to your database though Turso CLI and run them

```sql
CREATE TABLE User (
    user_id INTEGER PRIMARY KEY,
    clerk_user_id TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
);

CREATE TABLE Course (
    course_id INTEGER PRIMARY KEY,
    course_name TEXT,
    instructor TEXT,
    major_id INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (major_id) REFERENCES Major (major_id)
);

CREATE TABLE Review (
    review_id INTEGER PRIMARY KEY,
    user_id INTEGER,
    course_id INTEGER,
    difficulty_points INTEGER,
    usefulness_points INTEGER,
    comment TEXT,
    course_content TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES User (user_id),
    FOREIGN KEY (course_id) REFERENCES Course (course_id)
);

CREATE TABLE Major (
    major_id INTEGER PRIMARY KEY,
    major_name TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
);
```

## Contribuitors

- René Cáceres ([@panquequelol](https://github.com/panquequelol)) - currently developing the whole project alone :^(, feel free to reach out if you want to help me.