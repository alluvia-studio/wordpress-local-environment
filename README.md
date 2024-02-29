# Setting Up a Local Containerized WordPress Development Environment

Welcome to our WordPress local development environment configuration! This setup utilizes containerization technology, which allows developers to package applications and their dependencies into portable units called containers. With containerization, you can run WordPress projects consistently across different environments without worrying about system differences or configurations.

## Why Containerization?

Containerization offers several benefits for developing and managing multiple WordPress projects:

- **Isolation**: Each WordPress project runs independently within its own container, preventing conflicts between different versions or configurations.
- **Consistency**: It's easy to replicate the development environment across team members or machines, ensuring everyone works on the same setup.
- **Efficiency**: Containers are lightweight and efficient, requiring fewer resources compared to traditional virtual machines.

## Getting Started

If you're new to containerization or Docker, don't worry! Follow these simple steps to set up your local WordPress environment:

1. **Install Docker**: Download and install Docker from [here](https://docs.docker.com/get-docker/).

2. **Clone the Repository**: Clone this repository to your local machine.

```sh 
git clone https://github.com/alluvia-studio/wordpress-local-environment.git
```

3. **Spin up the Environment**: Open your terminal and navigate to the cloned repository directory. Then, run the following command:

```sh
cd wordpress-local-environment
docker compose up -d
```

4. **Grant Permissions (if necessary)**: Depending on your operating system, you may need to grant permissions to access certain directories. Follow the instructions below if you encounter any permission issues.

- For Linux:

```sh
sudo useradd -G <groupname> <username>
sudo chmod -R g+rwx ./wordpress/
```

- For macOS:

```sh
sudo dseditgroup -o edit -a <username> -t user <groupname>
```

5. **Theme Setup**: Copy or create your WordPress theme project in `./wordpress/wp-content/themes/<theme>`. If needed, add a symlink to the theme in the project's root directory. Make sure to exclude your theme from version control by updating the `.gitignore` file as shown below:

```plaintext
# .gitignore

wordpress/*
!wordpress/README.md
!wordpress/wp-content/

wordpress/wp-content/*
!wordpress/wp-content/themes/

wordpress/wp-content/themes/*
!wordpress/wp-content/themes/<theme>
```

6. **Adjust Upload File Size**: To increase the maximum upload file size, ensure you have a `.htaccess` file in `./wordpress/` with the following content:

```plaintext
php_value upload_max_filesize 256M
php_value post_max_size 256M
php_value max_execution_time 300
php_value max_input_time 300
```

Ta-da! Your local WordPress development environment is now set up and ready for you to start building amazing websites. If you have any questions or encounter any issues, feel free to reach out to the development team for assistance. Happy coding! 🚀

## Spinning Down and Cleanup

Once you're done with your development work, you can spin down the Docker containers and clean up associated volumes using the following steps:

### Stop the Containers: In your terminal, navigate to the repository directory and run:

```sh
docker compose down
```

### Destroy Volumes (Optional): If you want to remove all associated volumes (e.g., database data), run:

```sh
docker volume prune
```

That's it! Your Docker containers are now stopped, and associated volumes are cleaned up. Your local environment is ready for the next session. If you have any questions or encounter any issues, feel free to reach out to the development team for assistance. Happy coding! 🚀
