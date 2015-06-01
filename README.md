# What?

I want a Web service to catch and respond to a Web hook from a Docker Hub automated build
(https://docs.docker.com/docker-hub/builds/#webhooks). At a minimum, I want to be able to
trigger an update of an AWS ECS container as a result of a successful Docker image build on
Docker Hub. This means that I can commit to a repo which backs a public Docker image (like one
hosting a public API or website I'm developing) and have that pushed to ECS as soon as possible.

# How?

I'm going to try to use Go to do this. Because the webservice itself is relatively simple,
I think I can write a single method to catch the request, do some AWS API calls, and respond
with status.

AWS has a Go API, but it's not necessarily production ready. Thankfully, neither is this server. ;)

I want to run this service in a Docker container (YO DAWG), and I'll probably assume that this
container is itself running on ECS (but of course, that's not stricly necessary ... this is
Docker we're talking about).

# Why not Travis/my fave CI tool?

I like the transparency of the automated (official) Docker Hub build, and I don't want to roll my
own version of that build or its supporting infrastructure. I also don't want to host my own copy
of something like Jenkins (and I do love Jenkins!), because I don't need something that heavy.

# Implementation Log

## Initial Commit

I'm adding a super simple Web service example in Go, and a README.

## The Go AWS ECS API

Read this: http://godoc.org/github.com/awslabs/aws-sdk-go/service/ecs

## The Docker Hub Webhook Format

https://docs.docker.com/docker-hub/builds/#webhooks
