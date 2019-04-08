# Ops philosophy & goal

Today our infrastructure is mainly hosted by AWS.
We really don't want to use their services in the long run. We are only using them today because it's free (startup credits) and working with no effort (good service).
As a projection (that can be useful in the understanding of daily choices), we want to have our own datacenter(s) in a few years.

To be sure not to be locked on AWS, we follow some practices:
- only use standard technologies on AWS (PostgresSQL on RDS (and not Aurora) for example)
- if we have to use something in a non standard way (Amazon SES as an API for example), we build everything with the idea we'll leave them in mind. So that it should be really easy to move to another one. Concretly, that means we need to use interfaces and just have one implementation of the interface that correspond to AWS.


## Projections

We have some ops projects we want to achieve at a moment:

### Metrics everywhere

We want to have metrics dashboards in every business variables making sense to monitor

### Progressive deployments

When we release a new feature, it's progressively deployed to a batch of users (beta testers), then to 1% of all users, then 10%, then 100%.
Between each step, we follow the evolution of the metrics (if a bug do better results: we want keep it ! And if a feature make the usability harder we want to rethink it)

### Chaos monkey (Netflix inspiration)
