# Agent Instructions

## Toolchain

- Use the checked-in Gradle wrapper (`./gradlew`) with JDK 17; this is a JVM library, not an Android app module.
- Manage dependency versions in `gradle/libs.versions.toml`.

## Commands

| Task | Command |
| --- | --- |
| Compile library and regenerate parser registry | `./gradlew :compileKotlin` |
| Run one test class | `./gradlew :test --tests 'org.koitharu.kotatsu.parsers.util.PaginatorTest'` |
| Run live-site parser tests (select sources first) | `./gradlew :test --tests 'org.koitharu.kotatsu.parsers.MangaParserTest'` |
| Generate HTML from existing test results | `./gradlew :generateTestsReport` |

## Key Conventions

- Follow `CONTRIBUTING.md` for parser contracts, domain configuration, IDs, pagination, and HTML helpers.
- Look for a matching shared engine under `src/main/kotlin/org/koitharu/kotatsu/parsers/site/` before adding a standalone parser.
- Keep language-specific parsers in the matching language subdirectory of `src/main/kotlin/org/koitharu/kotatsu/parsers/site/`.
- Consult API documentation in `src/main/kotlin/org/koitharu/kotatsu/parsers/MangaParser.kt` when implementing parser methods.

- Change parser annotations or `kotatsu-parsers-ksp/src/main/kotlin/org/koitharu/kotatsu/parsers/ksp/ParserProcessor.kt`, not generated registry code under `build/generated/ksp/main/kotlin/`.
- Regenerate `.github/summary.yaml` through KSP compilation; do not edit its source count by hand.

- Tests live in `src/test/kotlin/`; prefer a relevant class filter over the entire suite.
- Before running `MangaParserTest`, temporarily select source enum names in `src/test/kotlin/org/koitharu/kotatsu/parsers/MangaSources.kt`; its `INCLUDE` list is empty by default.
- Restore temporary source-selection changes before submitting.
- Live-site tests require network access and can fail due to authentication, Cloudflare, or source availability.
- Custom HTML reports are written to `build/test-results-html/` from existing `build/test-results/test/` results.

## External References

| Need | File |
| --- | --- |
| Library usage and Android integration | `README.md` |
| Contribution and parser implementation guide | `CONTRIBUTING.md` |
| Parser class diagram | `docs/parser_classes.png` |
| Build and code generation configuration | `build.gradle.kts` |
