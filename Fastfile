# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

default_platform(:ios)

platform :ios do
  desc "Push a new beta build to TestFlight"
  lane :test do
    build_number = latest_testflight_build_number + 1

    increment_build_number(xcodeproj: "project_name.xcodeproj",
    build_number: build_number)

    get_certificates           # invokes cert
    get_provisioning_profile   # invokes sigh
    build_app(workspace: "workspace_name.xcworkspace", scheme: "project schema name")
    upload_to_testflight(changelog: "Testflight build description",
	distribute_external: true,
    distribute_only: false,
    groups: ["public link"])

    slack(message: "App has been successfully released!", slack_url: "slack url")

    # Clean folders
    clean_build_artifacts    
  end

  lane :production do
    build_number = latest_testflight_build_number + 1

    increment_build_number(xcodeproj: "project_name.xcodeproj",
    build_number: build_number)

    get_certificates           # invokes cert
    get_provisioning_profile   # invokes sigh
    build_app(workspace: "project_name.xcworkspace", scheme: "schema name")
    upload_to_testflight(changelog: "Production URL",
	distribute_external: true,
    distribute_only: false,
    groups: ["Public link"])

    slack(message: "Gasable-Production has been successfully released!", slack_url: "slack url")

    # Clean folders
    clean_build_artifacts    
  end
end
