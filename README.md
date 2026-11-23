 ნაწილი 1 — Docker კონტეინერები

 1. Hello World კონტეინერის გაშვება

docker run hello-world

გავუშვი სატესტო კონტეინერი Docker-ის მუშაობის შესამოწმებლად.

 2. Ubuntu კონტეინერის გაშვება

docker run -it ubuntu bash

გავუშვი Ubuntu ინტერაქტიულ რეჟიმში.

 3. curl-ის ინსტალაცია

apt update

apt install -y curl

curl -I https://www.google.com

დავაყენე curl და შევამოწმე ინტერნეტთან კავშირი.
 4. კონტეინერიდან გამოსვლა

exit
გამოვედი Ubuntu კონტეინერიდან.

 5. კონტეინერების მართვა
docker ps -a
docker stop CONTAINER_ID
docker rm CONTAINER_ID

გამოვიტანე კონტეინერების სია. გაჩერებისა და წაშლის ბრძანებები გამოიყენება საჭიროების შემთხვევაში.

 ნაწილი 2 — Python Docker იმიჯი

1. პროექტის შექმნა 
mkdir docker-python-app
cd docker-python-app

შევქმენი სამუშაო საქაღალდე.

 2. Python ფაილის შექმნა

app.py

print("Hello from my Python Docker container!")
print("My first Docker application is running!")

შევქმენი მარტივი Python პროგრამა.

 3. Dockerfile-ის შექმნა

FROM python:3.12-slim
WORKDIR /app
COPY app.py .
CMD ["python", "app.py"]

შევქმენი Dockerfile Python აპლიკაციისთვის.

 4. იმიჯის აწყობა

docker build -t my-python-app .

ავაწყვე Docker იმიჯი.

 5. კონტეინერის გაშვება

docker run --name my-python-container my-python-app

გავუშვი Python აპლიკაცია კონტეინერში.

 6. იმიჯის თეგი

docker tag my-python-app my-python-app:v1
docker images

მივანიჭე იმიჯს თეგი და გამოვიტანე იმიჯების სია.

 ნაწილი 3 — Docker Volumes

 1. Volume-ის შექმნა

docker volume create my-data-volume
docker volume ls

შევქმენი სახელდებული Volume.

 2. კონტეინერის გაშვება Volume-ით

docker run -it --name volume-container1 -v my-data-volume:/data ubuntu bash

მივაბი Volume Ubuntu კონტეინერს.

3. ფაილის შექმნა

echo "This file is saved in Docker Volume" > /data/test.txt
cat /data/test.txt

შევქმენი და შევინახე ფაილი Volume-ში.

 4. კონტეინერის წაშლა

exit
docker rm volume-container1

წავშალე პირველი კონტეინერი.

 5. მონაცემების შენარჩუნების შემოწმება

docker run -it --name volume-container2 -v my-data-volume:/data ubuntu bash
cat /data/test.txt

მეორე კონტეინერიდან შევამოწმე შენახული ფაილი.


თითოეული ნაბიჯის შესრულების შედეგები წარმოდგენილია screenshotsსაქაღალდეში.
