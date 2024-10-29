FROM python:3.9
# fix typo "appp" -> "app" 
WORKDIR /app  
# fix typo "appy.py" -> "app.py"
COPY app.py /app
# Fixed the package name netiface -> netifaces
RUN pip install flask netifaces
#  fix typo "eight thousand" -> 8000
EXPOSE 8000 
# Fixed the typo in CMD from "pythn" -> "python"
CMD ["python", "app.py"]
