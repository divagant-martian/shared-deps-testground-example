FROM rust:1.65-bullseye as builder
WORKDIR /usr/src/test-plan

RUN apt-get update

# Accept the PLAN_PATH parameters that is passed by testground.
ARG PLAN_PATH

COPY . .

RUN cd ./plan/${PLAN_PATH}/ && cargo build --release

FROM debian:bullseye-slim
COPY --from=builder /usr/src/test-plan/plan/target/release/plan_b /usr/local/bin/plan_b

ENTRYPOINT ["plan_b"]