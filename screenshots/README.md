 ნაწილი 1 — Docker კონტეინერები

 1. Hello World კონტეინერის გაშვება

docker run hello-world

![Hello World](screenshots/Screenshot 2026-11-23 173822.png)

გავუშვი სატესტო კონტეინერი Docker-ის მუშაობის შესამოწმებლად.

 2. Ubuntu კონტეინერის გაშვება

docker run -it ubuntu bash

გავუშვი Ubuntu ინტერაქტიულ რეჟიმში.
![Ubuntu](screenshots/Screenshot 2026-11-23 173855.png)
 3. curl-ის ინსტალაცია

apt update
![apt update](screenshots/Screenshot 2026-11-23 173950.png)
apt install -y curl
![curl installation](screenshots/Screenshot 2026-11-23 174053.png)

curl -I https://www.google.com
![Internet Check](screenshots/Screenshot 2026-11-23 174149.png)
დავაყენე curl და შევამოწმე ინტერნეტთან კავშირი.
 4. კონტეინერიდან გამოსვლა

exit
გამოვედი Ubuntu კონტეინერიდან.
![Exit Container](screenshots/Screenshot 2026-11-23 174202.png)
 5. კონტეინერების მართვა
docker ps -a
![Container List](screenshots/Screenshot 2026-11-23 174224.png)

docker stop CONTAINER_ID
![Stop Container](screenshots/Screenshot 2026-11-23 174255.png)
![Stop Result](screenshots/Screenshot 2026-11-23 174323.png)
docker rm CONTAINER_ID
![Remove Container](screenshots/Screenshot 2026-11-23 174327.png)
![Container Check](screenshots/Screenshot 2026-11-23 174342.png)
გამოვიტანე კონტეინერების სია. გაჩერებისა და წაშლის ბრძანებები გამოიყენება საჭიროების შემთხვევაში.

 ნაწილი 2 — Python Docker იმიჯი

1. პროექტის შექმნა ( ეს აპლიკაცია vs code ტერმინატლით შევქმენი უფრო გამიმარტივდა)

mkdir docker-python-app
cd docker-python-app
code .
![Project Creation](screenshots/Screenshot 2026-11-23 181338.png)
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
![Docker Build](screenshots/Screenshot 2026-11-23 181411.png)
ავაწყვე Docker იმიჯი.

 5. კონტეინერის გაშვება

docker run --name my-python-container my-python-app
![Python Container](screenshots/Screenshot 2026-11-23 181411.png)
გავუშვი Python აპლიკაცია კონტეინერში.

 6. იმიჯის თეგი

docker tag my-python-app my-python-app:v1
docker images
![Docker Tag](screenshots/Screenshot 2026-11-23 181754.png)

![Docker Images](screenshots/Screenshot 2026-11-23 181723.png)
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

![Docker Volume](screenshots/Screenshot 2026-11-23 181450.png)
cat /data/test.txt

მეორე კონტეინერიდან შევამოწმე შენახული ფაილი.


თითოეული ნაბიჯის შესრულების შედეგები წარმოდგენილია screenshotsსაქაღალდეში.

