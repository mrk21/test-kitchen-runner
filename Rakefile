DOCKER_NAME = "test-kitchen-runner"

namespace :docker do
  desc 'Build a Docker image'
  task :build do
    sh "docker build -t #{DOCKER_NAME} ."
    sh "docker rmi $(docker images | awk '/^<none>/ { print $3 }') 2> /dev/null || echo"
  end
  
  desc 'Run the built Docker image'
  task :run do
    sh "docker rm -f #{DOCKER_NAME} 2> /dev/null || echo"
    sh "docker run -itd --name=#{DOCKER_NAME} --privileged=true #{ENV['opt']} #{DOCKER_NAME}"
  end
  
  desc 'Execute a shell in the container'
  task :shell do
    sh "docker exec -it #{DOCKER_NAME} su -l -c '/bin/bash -i -l'"
  end
end
