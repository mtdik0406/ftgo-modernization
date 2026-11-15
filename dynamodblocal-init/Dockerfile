FROM python:2.7.16-alpine3.9
# PyYAML 5.x のビルドが Cython 3 で失敗するため、Cython 3 未満を入れてから build isolation なしで PyYAML を入れる
RUN pip install "cython<3" && pip install --no-build-isolation "pyyaml<5.5" && pip install "awscli==1.19.112"
COPY create-dynamodb-tables.sh .
COPY ftgo-order-history.json .
COPY wait-for-dynamodblocal.sh .
RUN chmod +x *.sh
HEALTHCHECK --interval=10s --retries=10 --timeout=3s CMD [[ -f /tables-created ]]

CMD ./wait-for-dynamodblocal.sh && ./create-dynamodb-tables.sh
