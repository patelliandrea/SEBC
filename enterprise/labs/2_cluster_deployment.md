```json
{
  "timestamp" : "2016-11-16T09:58:55.882Z",
  "clusters" : [ {
    "name" : "patelliandrea",
    "version" : "CDH5",
    "services" : [ {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "SERVER",
          "items" : [ {
            "name" : "zookeeper_server_java_heapsize",
            "value" : "639631360"
          } ]
        } ],
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-3874eb23113210ba1ba049ac51a9a099",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "dnjreoa3ddzuh2mpqxkxq7nhh"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "64zp6w9yhfv1zvuk1rcj301t5"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-bc638057420c5c30b6e3071f78420cd8",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4xrgxnm4h7ea93sq2on6s9qt1"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "OOZIE_SERVER",
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "ip-172-20-0-4.eu-central-1.compute.internal"
          }, {
            "name" : "oozie_database_name",
            "value" : "hue"
          }, {
            "name" : "oozie_database_password",
            "value" : "hue"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "hue"
          }, {
            "name" : "oozie_java_heapsize",
            "value" : "639631360"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5pqlrtnfops5wz20gotsvjloi"
          } ]
        }
      } ],
      "displayName" : "Oozie"
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ {
          "name" : "database_host",
          "value" : "ip-172-20-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "database_password",
          "value" : "hue"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-HTTPFS-3874eb23113210ba1ba049ac51a9a099"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "6e7hsptojy9eivvlmclaxuf28"
          }, {
            "name" : "secret_key",
            "value" : "T3d1j4ZES3vYMnNpQFKuxP2kKRu541"
          } ]
        }
      } ],
      "displayName" : "Hue"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "BALANCER",
          "items" : [ {
            "name" : "balancer_java_heapsize",
            "value" : "639631360"
          } ]
        }, {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "datanode_java_heapsize",
            "value" : "1073741824"
          }, {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "10736157900"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4294967296"
          }, {
            "name" : "rm_cpu_shares",
            "value" : "200"
          }, {
            "name" : "rm_io_weight",
            "value" : "100"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "JOURNALNODE",
          "items" : [ {
            "name" : "dfs_journalnode_edits_dir",
            "value" : "/dfs/jn"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/dfs/snn"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_client_use_datanode_hostname",
          "value" : "true"
        }, {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "72RTqNT0qlYc6ewF4KLXodv4EPLwMt"
        }, {
          "name" : "dfs_ha_fencing_methods",
          "value" : "shell(true)"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "jyyvUKq7oacHgBVru86rzTpDCl7rpJ"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "0hVozac1vbWI6Zvn5uLScMOXkIaO3c"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "10"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-bc638057420c5c30b6e3071f78420cd8",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-2e0d50c63a99bec3527867f9fe553e58",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-3cb82281"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "55si9i1vzdyhggp32dp9ry9r4"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-3874eb23113210ba1ba049ac51a9a099",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3x6u0ta3nk0327iaf36j4se8j"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "dm0k1k8rb372jpjs54pk5b8ko"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-8f2c37d193a13d6371c31bdc972a032b",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "i-3db82280"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "apcc6by4vpq76e404vkcc6r8y"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-3874eb23113210ba1ba049ac51a9a099",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9wqwhniz1hb583svyxz5vk40g"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-bc638057420c5c30b6e3071f78420cd8",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2uoa6gssb8o1nzo78j5lqp0y1"
          } ]
        }
      }, {
        "name" : "hdfs-HTTPFS-3874eb23113210ba1ba049ac51a9a099",
        "type" : "HTTPFS",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "587pukkvrd78szfcrzkeylxf2"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-3874eb23113210ba1ba049ac51a9a099",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_health_suppression_journal_node_fsync_latency",
            "value" : "true"
          }, {
            "name" : "role_jceks_password",
            "value" : "66drt0u3tcfyzb7by58s25kb3"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2ed7f61tieizkh0vuw7vlb5td"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-bc638057420c5c30b6e3071f78420cd8",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7dpmr2fwkx0nr4k68ymqoffk8"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-3874eb23113210ba1ba049ac51a9a099",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "70"
          }, {
            "name" : "role_jceks_password",
            "value" : "70x9u9u42kmwhn4l23f3vnhdi"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-bc638057420c5c30b6e3071f78420cd8",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "nameservice1"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "nameservice1"
          }, {
            "name" : "namenode_id",
            "value" : "46"
          }, {
            "name" : "role_jceks_password",
            "value" : "c0b4tpckzj9lphqymknr0es9z"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "8"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "2"
          } ]
        }, {
          "roleType" : "JOBHISTORY",
          "items" : [ {
            "name" : "mr2_jobhistory_java_heapsize",
            "value" : "639631360"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "rm_cpu_shares",
            "value" : "1800"
          }, {
            "name" : "rm_io_weight",
            "value" : "900"
          }, {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "3"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "1024"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "resource_manager_java_heapsize",
            "value" : "639631360"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "4938"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "3"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "90"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "Tc4wTLbEewMo46JPXIzW3pPhQGbxjP"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-GATEWAY-bc638057420c5c30b6e3071f78420cd8",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "yarn-JOBHISTORY-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "f1lbpga4t5huosb3w6v06459r"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-2e0d50c63a99bec3527867f9fe553e58",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-3cb82281"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "a43ehnyby9t6s34vcdiouzkb"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-3874eb23113210ba1ba049ac51a9a099",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5f8rrvigr34x0kbi01uuanpf9"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "ab1x810djexoexspjbnq0ogsj"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-8f2c37d193a13d6371c31bdc972a032b",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "i-3db82280"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "d411dk0gisy4ftdubphywrcn2"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "68"
          }, {
            "name" : "role_jceks_password",
            "value" : "b05tgpqiescufy1pvil3knbyh"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "639631360"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "639631360"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "2288831692"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "385"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "ip-172-20-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-2e0d50c63a99bec3527867f9fe553e58",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-3cb82281"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-3874eb23113210ba1ba049ac51a9a099",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-5bd43db47d665077a0c0d5aa07db2e73",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-8cbe2431"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-8f2c37d193a13d6371c31bdc972a032b",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-3db82280"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-bc638057420c5c30b6e3071f78420cd8",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-92be242f"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-3874eb23113210ba1ba049ac51a9a099",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "eha334wdjayrpizm2mjp5zpd6"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-3874eb23113210ba1ba049ac51a9a099",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "i-8dbe2430"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "eat41zwu9e7lfo7upgntef5na"
          } ]
        }
      } ],
      "displayName" : "Hive"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "i-92be242f",
    "ipAddress" : "172.20.0.4",
    "hostname" : "ip-172-20-0-4.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-8dbe2430",
    "ipAddress" : "172.20.0.5",
    "hostname" : "ip-172-20-0-5.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-8cbe2431",
    "ipAddress" : "172.20.0.6",
    "hostname" : "ip-172-20-0-6.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-3db82280",
    "ipAddress" : "172.20.0.7",
    "hostname" : "ip-172-20-0-7.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "i-3cb82281",
    "ipAddress" : "172.20.0.8",
    "hostname" : "ip-172-20-0-8.eu-central-1.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-bc638057420c5c30b6e3071f78420cd8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "c750c398e31962c9858bd1edd2058c7d4857a70618721d553f9b93b59f0b31db",
    "pwSalt" : -5658968975557412678,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-bc638057420c5c30b6e3071f78420cd8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "9f9e168db462d70de0d4bcd168f6fa339ca849d4f6b4c81ead946d812ee3ad61",
    "pwSalt" : 7470445111388540732,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-bc638057420c5c30b6e3071f78420cd8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "bd01b6e5a95a49e45b0ff9a00a4ac8ee8d761b441c3210880dadb0c0c571329e",
    "pwSalt" : 5174475040689421589,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-bc638057420c5c30b6e3071f78420cd8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "51de0e74522ac76e8c58945d8c8d9f79cc309e733be9712c984edde58cf46083",
    "pwSalt" : 8400907139427859181,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "bf64087c78c7909c7fe99955a1e9d331b9033bfe926dc4edc9030f600bdec230",
    "pwSalt" : -3933840232426849032,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "8bb14edbce49e11f6f06ed53ea4f4a1bb31707d786d57372c8fd30f129ac2d03",
    "pwSalt" : -4534005802886211860,
    "pwLogin" : true
  }, {
    "name" : "patelliandrea",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "e54b38a52b35c792e2a16ab87ff17eef494e3de7a5c902ad8da676b1468ed9f5",
    "pwSalt" : 6686802724239374854,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.9.0",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20161006-1801",
    "gitHash" : "898a5e032c080e18833dfc58180761f6ef2ea351",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "EVENTSERVER",
        "items" : [ {
          "name" : "event_server_heapsize",
          "value" : "639631360"
        } ]
      }, {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "639631360"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "831520768"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "ip-172-20-0-4.eu-central-1.compute.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        }, {
          "name" : "headlamp_heapsize",
          "value" : "639631360"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_heapsize",
          "value" : "639631360"
        }, {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "831520768"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ALERTPUBLISHER-bc638057420c5c30b6e3071f78420cd8",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "i-92be242f"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "dz66422kb3woei69z7351h9xb"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-bc638057420c5c30b6e3071f78420cd8",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "i-92be242f"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "5ra6hzzhoxidzdgneyfpslq32"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-bc638057420c5c30b6e3071f78420cd8",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "i-92be242f"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "3l4it1g06751j4p25y6wbddd5"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-bc638057420c5c30b6e3071f78420cd8",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "i-92be242f"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "aucj0nigfkrrxs0gempbkv4vz"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-bc638057420c5c30b6e3071f78420cd8",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "i-92be242f"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "7yt7qajn4gm9x23nysvjs4jz9"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/23/2012 18:50"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/{latest_supported}/,https://archive.cloudera.com/cdh4/parcels/latest/,https://archive.cloudera.com/impala/parcels/latest/,https://archive.cloudera.com/search/parcels/latest/,https://archive.cloudera.com/accumulo/parcels/1.4/,https://archive.cloudera.com/accumulo-c5/parcels/latest/,https://archive.cloudera.com/kafka/parcels/latest/,https://archive.cloudera.com/navigator-keytrustee5/parcels/latest/,https://archive.cloudera.com/sqoop-connectors/parcels/latest/,http://ip-172-20-0-8.eu-central-1.compute.internal/local_repo"
    } ]
  }
}
```