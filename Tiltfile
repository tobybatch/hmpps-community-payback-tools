docker_compose("./compose.yml")

resources = [
    "hmpps-auth-upw",
]

local_resource(
    "api-local",
    serve_cmd="./gradlew bootRun --stacktrace --args='--spring.profiles.active=localdev'",
    # Note! These checks only wait for containers to start, ideally we'd wait for them to be ready
    # see https://docs.tilt.dev/resource_dependencies.html
    # "For dc_resource: the container is started (NB: Tilt doesn’t currently observe docker-compose health checks)"
    resource_deps=["hmpps-auth-upw"],
    serve_dir=os.getenv("LOCAL_UPW_API_PATH"),
    readiness_probe=probe(
    initial_delay_secs=10,
    period_secs=5,
    timeout_secs=2,
    http_get=http_get_action(
        port=8080,
        path="/health"
    )
    )
)
resources.append("api-local")

local_resource(
    "upw-ui-local",
    cmd="npm install",
    serve_cmd="npm run start:dev",
    resource_deps=["api-local"],
    serve_dir=os.getenv("LOCAL_UPW_UI_PATH"),
    dir=os.getenv("LOCAL_UPW_UI_PATH"),
    readiness_probe=probe(
        period_secs=15, http_get=http_get_action(port=3000, path="/health")
    )
)
resources.append("upw-ui-local")
