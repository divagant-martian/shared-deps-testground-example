# Get chef
FROM rust:1.65-bullseye as chef
WORKDIR test-plan
RUN cargo install cargo-chef

# Get chef to create a skeleton workspace
FROM chef AS planner
COPY ./plan .
RUN cargo chef prepare --recipe-path recipe.json

FROM chef as builder
# Build dependencies
# RUN apt-get update && apt-get -y upgrade && apt-get install -y protobuf-compiler
COPY --from=planner /test-plan/recipe.json recipe.json

# Cache the deps using the fake workspace
RUN cargo chef cook --release --recipe-path recipe.json

# Get the real code. 
COPY ./plan .

# Build the package
# NOTE: from chef's docs: the cook and build commands need to be run from the
# same dir. So we use the root dir to get all the deps right.
RUN cargo build --release -p plan_a

FROM debian:bullseye-slim

COPY --from=builder /test-plan/target/release/plan_a /usr/local/bin/plan_a

# Set env variables
# ENV RUST_LOG=libp2p_gossipsub=debug

ENTRYPOINT ["plan_a"]
