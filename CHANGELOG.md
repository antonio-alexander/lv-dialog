# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2020-12-28

- Introduced two (see below) breaking changes, it's not really worth creating a new API (my apologies if this actually affects you)
- (1) Updated the busy_wait event to be more extensible, this is semi-forward compatible, but instead of having a baked in event registration for a boolean "done", it's a variant that can be casted into a known event registration reference that can contain anything the caller wants to implement.
- (2) Added additional VIs to the feedback to simplify its api and not provide "process" error as a separate input

## [1.0.0] - 2020-12-16

- Completed first iteration of both lv-dialog and lv-dialog-interfaces, see documentation for uses
