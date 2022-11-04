FROM rust:1.65-bullseye as builder
WORKDIR /usr/src/test-plan

RUN apt-get update 

RUN mkdir -p ./plan/src/

# This is a placeholder main function to build only the dependencies.
RUN echo "fn main() { println!(\"If you see this message, you may want to clean up the target directory or the Docker build cache.\") }" > ./plan/src/main.rs
COPY ./plan/Cargo.toml ./plan/
RUN cd ./plan/ && cargo build --release


COPY . .

RUN touch ./plan/src/main.rs

# Note: In `docker:generic` builder, the root of the docker build context is one directory higher
# than this test plan.
# See https://docs.testground.ai/builder-library/docker-generic#usage
RUN cd ./plan/ && cargo build --release

FROM debian:bullseye-slim
COPY --from=builder /usr/src/test-plan/plan/target/release/plan_a /usr/local/bin/plan_a

ENTRYPOINT ["plan_a"]
