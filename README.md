# What is Miku Notes?

As the name might suggest, the app's main purpose is to store and manage personal notes. More features will be listed soon.

This app consists of four main parts, three microservices and the frontend:
- [Auth service](https://github.com/kuromii5/miku-notes-auth)
- [Data service](https://github.com/kutoru/miku-notes-data)
- [Gateway service](https://github.com/kutoru/miku-notes-gateway)
- [Frontend](https://github.com/kinokorain/miku-notes-frontend)

To learn more about each individual part, you can go into its repository and explore the readme there

# How to run it locally?

In the near future, you'll be able to just fill out the [.env](#env) file, and then compose and run the Docker containers. But for now, you'll have to go into each part individually, and follow the instructions there. Also note that since the **Frontend** isn't yet finished, the only way to interact with the app is through its API. To see all the available API routes, check the **Gateway service**'s readme

# .env

An example .env configuration is included in the repository. Explanations for each value will be added as soon as the Docker containerization gets finished
