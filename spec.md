# Sandthorn Event Format

The Sandthorn Event Sourcing System concists of:

  - Sandthorn client (e.g. the sandthorn ruby gem)
  - One or more Event Stores
  - Optional plugins, such as snapshotting systems

## Purpose

The Sandthorn Event Format specifies the format of events that are delivered from a Sandthorn Event Store through the Sandthorn client.
Events may be stored in another format in the Event Store, but must always be served back in this format.

## Format

A Sandthorn event is a map of keys and values. 

### Root Level

The root level of an event has the following format:

    aggregate_version [required] :: Integer
    aggregate_id [required] :: String
    aggregate_type [required] :: String
    sequence_number [required] :: Integer
    name [required] :: String
    server_timestamp [required] :: ISO8601 format String OR language native Date/Time format
    client_timestamp [optional] :: ISO8601 format String OR language native Date/Time format
    meta [optional] :: Map
    attribute_deltas [required] :: Array

#### Attribute deltas

The value of the `attribute_deltas` key must be an an empty array or an array of maps, each map representing a changed attribute. Each map has the following format:

    attribute_name [required] :: String
    old_value [required] :: Any
    new_value [required] :: Any

#### Meta

The value of the `meta` key must a map. The purpose of the meta map is to hold meta information such as event/method arguments or trace information. It may contain any valid data.

## Valid types of data

TODO: we may have to restrict the kinds of data that can be saved in an event.
